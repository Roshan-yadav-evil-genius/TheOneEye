Below are **multiple Mermaid diagrams** that together explain the Workflow Engine **end-to-end** — design time, runtime, validation, looping, and frontend–backend interaction.
Each diagram focuses on **one architectural concern**, so reviewers can reason about the system in layers.

---

## 1. High-Level System Architecture

**Purpose:** Shows major components and responsibility boundaries.

```mermaid
flowchart LR
    UI[ReactFlow Frontend]
    API[Workflow Backend API]
    VAL[Validation Engine]
    DB[(Workflow DB)]
    EXEC[Execution Engine]
    Q[Queue / Redis]
    WORKERS[Worker Processes]

    UI -->|User Actions| API
    API --> VAL
    VAL -->|Valid| DB
    API -->|Execute| EXEC
    EXEC --> Q
    Q --> WORKERS
```

**Key Takeaway:**
Frontend never decides correctness. Backend validates, persists, and executes.

---

## 2. Design-Time Interaction Flow (Single Source of Truth)

**Purpose:** Explains incremental validation and persistence.

```mermaid
sequenceDiagram
    participant FE as Frontend
    participant BE as Backend
    participant V as Validator
    participant DB as Database

    FE->>BE: Add Node / Edge
    BE->>V: Validate mutation
    alt Valid
        V-->>BE: OK
        BE->>DB: Persist change
        DB-->>BE: Success
        BE-->>FE: Updated workflow state
    else Invalid
        V-->>BE: Error + Reason
        BE-->>FE: Validation error
    end
```

**Key Takeaway:**
Invalid workflow states are **never stored**.

---

## 3. Workflow Graph Model (Strict DAG)

**Purpose:** Shows that the workflow graph itself is always acyclic.

```mermaid
flowchart TD
    P[Producer]
    B1[Blocking Node]
    B2[Blocking Node]
    NB[Non-Blocking Node]

    P --> B1
    B1 --> B2
    B2 --> NB

    %% No edge allowed back to P
```

**Key Takeaway:**
There is **no cycle in the graph** — loops are not graph edges.

---

## 4. Loop Execution Model (Critical Concept)

**Purpose:** Demonstrates how loops work without graph cycles.

```mermaid
flowchart LR
    subgraph Single Loop Execution
        P[Producer]
        B1[Blocking]
        B2[Blocking]
        NB[Non-Blocking]
        P --> B1 --> B2 --> NB
    end

    NB -.->|Loop Restart| P
```

**Key Takeaway:**
Loop restart is an **execution jump**, not a graph connection.

---

## 5. Blocking vs Non-Blocking Semantics

**Purpose:** Explains execution path termination.

```mermaid
flowchart TD
    P[Producer]
    B[Blocking Node]
    NB[Non-Blocking Node]
    END[Path Ends]

    P --> B --> NB
    NB -->|Async push| END

    B -->|Synchronous| END
```

**Key Takeaway:**
Non-blocking nodes **terminate the current execution path**.

---

## 6. Execution Engine Runtime Flow

**Purpose:** Shows what happens during execution.

```mermaid
sequenceDiagram
    participant EE as Execution Engine
    participant W as Worker
    participant Q as Queue / Redis

    EE->>W: Start loop execution
    W->>W: Execute Blocking Nodes
    W->>Q: Push data (Non-Blocking)
    W-->>EE: Loop completed
    EE->>W: Restart loop from Producer
```

**Key Takeaway:**
Each loop iteration is isolated and deterministic.

---

## 7. Design-Time vs Execution-Time Validation

**Purpose:** Clarifies validation responsibilities.

```mermaid
flowchart LR
    DT[Design-Time Validation]
    ET[Execution-Time Validation]

    DT -->|Structural| Rules1[Graph rules\nSingle Producer\nNo cycles]
    ET -->|Semantic| Rules2[Reachability\nNo dangling paths\nExecutable nodes]
```

**Key Takeaway:**
Design-time ≠ execution-time. Both are mandatory.

---

## 8. Incomplete Workflow Lifecycle

**Purpose:** Shows how incomplete workflows are allowed but blocked from execution.

```mermaid
stateDiagram-v2
    [*] --> Draft
    Draft --> Draft: Add / Remove nodes
    Draft --> Invalid: Structural issue
    Draft --> Valid: Complete graph
    Valid --> Executable
    Invalid --> Draft
```

**Key Takeaway:**
Incomplete workflows are **saveable**, not **runnable**.

---

## 9. Node Availability Resolution (Dynamic UI)

**Purpose:** Explains backend-driven UI behavior.

```mermaid
sequenceDiagram
    participant FE as Frontend
    participant BE as Backend

    FE->>BE: Request available nodes (workflowId)
    BE->>BE: Evaluate graph constraints
    BE-->>FE: Allowed node types
```

**Example Rule Encoded in Backend:**

* Producer exists → Producer hidden
* Producer deleted → Producer allowed

---

## 10. End-to-End Execution View

**Purpose:** Full mental model from design to execution.

```mermaid
flowchart LR
    UI[ReactFlow UI]
    API[Backend API]
    DB[(DB)]
    EXEC[Execution Engine]
    WORKER[Worker]

    UI --> API --> DB
    UI -->|Execute| API --> EXEC --> WORKER
```

**Key Takeaway:**
Design and execution are cleanly separated but fully consistent.

---

## Final Mental Model

* **Graph = structure**
* **Loop = execution behavior**
* **Backend = authority**
* **Frontend = intent capture**
* **Validation = layered safety**
* **Execution = deterministic and isolated**