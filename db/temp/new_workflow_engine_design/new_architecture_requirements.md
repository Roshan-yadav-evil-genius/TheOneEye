# DAG Workflow Engine – New Architecture (Requirements)

Developer requirements reference for the DAG workflow engine. Use this document to implement and verify behavior.

---

## 1. Core Principles

- The system is based on a **Directed Acyclic Graph (DAG)**.
- The graph structure is static; execution is dynamic.
- There are no cycles in the graph; repetition is handled via re-execution (e.g. **End (Re-Execute)** or loop nodes).
- Every workflow execution is isolated, resumable, and deterministic.
- Parallelism and synchronization are explicitly configured by the user—never implicit.

---

## 2. Workflow Structure

- Every workflow has:
  - Exactly one **Start Node**.
  - One or more **End Nodes**.
- Every execution:
  - Starts at the **Start Node**.
  - Ends at an **End Node**.
- Each branch must terminate at an **End Node**.

---

## 3. Start Node (Entry Control)

- The **Start Node** defines how data enters the workflow; it does not run business logic.

**Supported Start Modes**

- **Empty**
  - Execution starts immediately.
  - Passes empty initial context downstream.
- **Webhook (Wait Mode)**
  - Execution is created in WAITING state.
  - Resumes when the webhook payload arrives.
- **From Another Workflow**
  - Triggered by an upstream workflow.
  - Payload is injected as initial context.
- **Code / Webhook (Dual Entry Mode)**
  - The same **Start Node** accepts internal API calls and external webhook requests.
  - Payload is normalized before execution.
  - Trigger source is stored only as metadata.

**Start Node Rules**

- Stateless.
- Never executes business logic.
- Does not block on downstream execution.
- Each trigger creates a new workflow execution.

---

## 4. Webhook Handling (Critical Design Rule)

- Webhook endpoints are stateless and non-blocking.
- The webhook does **not** execute workflow logic.

For each webhook request:

- Validate the payload.
- Create a new execution.
- Persist initial data.
- Return immediately (e.g. 200 OK).
- Execution is handled asynchronously by the scheduler/workers.
- Multiple webhook requests can arrive concurrently without loss.

---

## 5. Node Execution Model

- A node executes only when:
  - All required parent conditions are satisfied.
  - Routing rules allow execution.
- Node states: **PENDING** → **RUNNING** → **COMPLETED** / **FAILED** / **IGNORED**.
- Node outputs are append-only in the execution context.
- Nodes never mutate outputs of other nodes.

---

## 6. Conditional Routing

- **Condition Nodes** evaluate expressions on the execution context.
- Exactly one outgoing edge is activated at runtime.
- Non-selected branches are marked **IGNORED** (not failed).
- Conditional logic never creates graph cycles.

---

## 7. Parallel Execution & Synchronization

- Parallelism is explicitly configured by the user.

**Parallel Execution Configuration**

| Concern | Options |
|--------|--------|
| Execution mode | **SEQUENTIAL** (one after another), **PARALLEL** (execute concurrently) |
| Join strategy | **WAIT_ALL** (wait for all nodes), **WAIT_ANY** (proceed on first completion), **NO_JOIN** (fire-and-forget) |
| Result collection | Merge outputs; collect as array; use first result; custom mapping |

**Parallel Execution Rules**

- Parallel nodes execute independently.
- Join behavior is deterministic.
- Failures are handled per group configuration.
- There is no implicit waiting or auto-merging.

---

## 8. Loop Handling

- The graph remains acyclic at all times.
- Looping is handled via **Loop Nodes** only.

**Loop Node behavior**

- Iterates over data.
- Executes an internal sub-DAG per item.
- Aggregates results.
- Emits a single output downstream.
- The **Loop Node** is atomic from the outer DAG’s perspective.

---

## 9. End Node (Exit Control)

- **End Nodes** define what happens after execution completes.

**End Node Types**

- **End (Terminate)**
  - Marks execution as completed.
  - No further processing.
- **End (Re-Execute)**
  - Signals the engine to start a new execution.
  - New execution begins from the **Start Node**.
  - No graph cycles are created.
  - Optional delay/retry policy is a future extension.

**End Node Rules**

- End nodes do not connect back to the **Start Node** with an edge.
- Re-execution always creates a new execution instance.

---

## 10. Execution Engine

- The scheduler determines runnable nodes based on state.
- Workers execute nodes asynchronously.
- Supports parallel execution with configurable limits.
- Execution state is persisted after every node.
- The system can safely resume after crashes.

---

## 11. Execution Context & State

- Each execution has its own context.
- Context is immutable and append-only.
- It stores: inputs, node outputs, metadata.
- It enables: replay, debugging, auditability.

---

## 12. Workflow-to-Workflow Communication

- Workflows can trigger other workflows via:
  - **Start Node** (From Workflow mode).
  - Webhook / API trigger.
- Data is passed explicitly (e.g. into Start or webhook payload).
- Executions remain isolated between workflows.

---

## 13. Key Guarantees

- No lost webhook events.
- No hidden parallelism (all parallelism is explicit).
- No implicit retries (retry behavior is configured).
- No execution blocking at ingress (webhook returns immediately).
- Predictable, debuggable execution flow.
