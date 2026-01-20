# Workflow Engine – Full Architecture & Design Explanation

This document provides a **complete, end‑to‑end explanation** of the Workflow Engine system. It covers design-time behavior, runtime execution, validation philosophy, loop semantics, frontend–backend interaction, and architectural principles. This is intended as a **single source of truth** for developers, architects, and reviewers.

---

## 1. System Overview

The system is a **graph‑based Workflow Engine** that allows users to visually design workflows using a ReactFlow-based UI and execute them using a backend execution engine.

Key characteristics:

* Backend is the **single source of truth**
* Workflow is modeled as a **Directed Acyclic Graph (DAG)**
* Loops are **execution constructs**, not graph cycles
* Validation is **incremental at design time** and **comprehensive at execution time**
* The system supports **blocking and non‑blocking execution paths**

---

## 2. High‑Level Architecture

### Components

* **ReactFlow Frontend**

  * Visual canvas for workflow design
  * Stateless UI
  * Sends user intent to backend

* **Workflow Backend**

  * Validation engine
  * Persistence layer
  * Node availability resolver
  * Execution engine

* **Execution Infrastructure**

  * Worker processes
  * Redis / DB / Queue systems
  * Loop isolation per execution

---

## 3. Backend as Single Source of Truth

The backend owns **all workflow rules and state**.

* Frontend never assumes correctness
* Frontend state is always **rebuildable from DB**
* Every mutation is validated before persistence

This guarantees:

* Consistency
* Deterministic behavior
* No frontend–backend rule drift

---

## 4. Workflow Graph Model

### Core Rules

* Workflow graph is **strictly acyclic**
* Any attempt to create a cyclic edge is rejected
* All nodes and edges must pass validation before being stored

### Incremental Construction

Workflows are built **incrementally**:

* Invalid states are never persisted
* Each user action is validated independently

---

## 5. Node Types & Semantics

### 5.1 Producer Node

**Role:**

* Entry point of workflow execution
* Defines loop start

**Rules:**

* Exactly **one Producer per workflow**
* No incoming edges

---

### 5.2 SubProducer Node

**Role:**

* Specialized Producer
* Receives data from external systems (Redis, DB, etc.)

**Key Property:**

* Inherits Producer semantics
* Treated identically by execution engine

---

### 5.3 Blocking Node

**Role:**

* Executes synchronously
* Passes control to downstream nodes

**Examples:**

* Business logic
* Transformations
* Validations

---

### 5.4 Non‑Blocking Node

**Role:**

* Asynchronous execution boundary
* Terminates current execution path

**Behavior:**

* Pushes data to external system
* Triggers loop restart
* Does **not** execute downstream nodes

**Examples:**

* RedisPushNode
* DBPushNode

---

## 6. Loop Execution Model (Critical Concept)

### What a Loop Is

A loop is **not a graph cycle**.

A loop is:

* A linear execution path
* Starting from a Producer (or SubProducer)
* Ending at:

  * A Non‑Blocking node, OR
  * End of a branch (typically Blocking)

---

### Loop Lifecycle

1. Execution starts at Producer
2. Nodes execute sequentially
3. Execution ends at loop boundary
4. Engine restarts execution from the **same Producer**

### Key Properties

* Loop restart is **static** (never data‑dependent)
* Each loop runs in its **own process / context**
* Multiple loops do not block each other

---

## 7. Design‑Time Validation

Design‑time validation runs on every mutation:

* Node addition
* Edge creation
* Node deletion
* Edge deletion

### Design‑Time Rules

* Single Producer rule
* Incoming / outgoing compatibility
* Node placement rules
* Graph acyclic validation
* No hanging / incomplete nodes

### Outcome

* If validation passes → persist + return ID
* If validation fails → return error with reason

No execution semantics are evaluated at this stage.

---

## 8. Incomplete Workflow State

Workflows may exist in an **incomplete state** during design.

### Definition

A workflow is incomplete if:

* A node has missing required connections
* A branch terminates illegally
* Required inputs are unresolved

### Behavior

* Incomplete workflows can be saved
* Incomplete workflows **cannot be executed**
* Execution request triggers full validation

---

## 9. Execution‑Time Validation

Triggered only when user executes or publishes workflow.

### Execution‑Time Checks

* All nodes reachable from Producer
* No dangling branches
* Loop boundaries are valid
* Runtime feasibility of node execution

Failure at this stage blocks execution completely.

---

## 10. Node Availability Resolution

Available nodes in the frontend are **derived from backend state**.

### Flow

1. Frontend requests available nodes with workflowId
2. Backend evaluates workflow constraints
3. Backend removes disallowed node types
4. Frontend renders returned list

### Example

* After Producer is placed → Producer nodes disappear
* If Producer is deleted → Producer nodes reappear

---

## 11. Frontend–Backend Interaction Pattern

### Node Placement

```
Frontend → Place Node
Backend → Validate
        → Persist
        → Return ID
Frontend → Refresh Workflow State
```

### Edge Creation

```
Frontend → Create Edge
Backend → Validate (no cycles)
        → Persist
        → Return ID
Frontend → Refresh Workflow State
```

---

## 12. Execution Engine Responsibilities

* Traverse workflow graph
* Manage execution context per loop
* Handle blocking vs non‑blocking behavior
* Restart loops deterministically
* Isolate loop execution

Execution logic is **fully decoupled** from design‑time validation.

---

## 13. Architectural Principles

* **Single Source of Truth** – Backend owns all rules
* **Separation of Concerns** – Design vs execution
* **Explicit Control Flow** – No hidden cycles
* **Extensibility** – Node behavior via inheritance
* **Determinism** – Static loop restart

---

## 14. Summary

This Workflow Engine:

* Uses a strict DAG for safety
* Supports powerful looping via execution semantics
* Ensures correctness through layered validation
* Scales via non‑blocking, isolated execution
* Maintains clarity between design‑time and runtime concerns

The system is robust, extensible, and suitable for complex real‑world orchestration use cases.

---

This document can be used as:

* Architecture reference
* Onboarding guide
* Design review artifact
* Foundation for future extensions
