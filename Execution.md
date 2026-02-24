⚙️ Execution & Runtime — How Flows Actually Run
===============================================

This section explains **how Shaunebu Bot Orchestrator executes flows at runtime**.  
It covers the **execution lifecycle**, **runtime architecture**, **memory model**, and the **guarantees** that make execution deterministic, debuggable, and export-ready.

* * *

🔁 Execution Lifecycle
----------------------

Every bot execution follows a **strict, deterministic lifecycle**.

* * *

### ⚡ Trigger Resolution

Execution always starts by resolving a trigger:
1.  The runtime loads the target flow
    
2.  All trigger nodes are evaluated
    
3.  The **first matching trigger** fires
    
4.  Execution begins at the trigger’s `next` port
    
Triggers decide **whether** execution starts — not how it proceeds.

* * *

### 🚦 Node Dispatching

Once execution starts:
*   Nodes are executed **one at a time**
    
*   Each node:
    *   Receives the current execution context
        
    *   Evaluates its logic
        
    *   Returns a structured execution result
        
Node dispatching is **schema-driven**, not hard-coded.

* * *

### 🔀 Port Routing

Nodes do not decide the next node directly.
Instead, they return:
*   A **port ID** (`next`, `true`, `false`, `loop`, etc.)
    
*   Or a **direct node jump** (advanced cases)
    
The runtime resolves:

`(Current Node + Output Port) → Connection → Next Node`

This ensures:
*   Visual and runtime models stay aligned
    
*   Execution is predictable and traceable
    

* * *

### 🛑 Flow Termination

Execution ends when:
*   No next node can be resolved
    
*   A node returns `Stop`
    
*   A dialog stack fully unwinds
    
*   An unrecoverable error occurs
    
Flow termination is explicit — never implicit.

* * *

🧱 Runtime Architecture
-----------------------

The runtime is intentionally **simple, explicit, and extensible**.

* * *

### 🧠 GraphFlowRuntime

`GraphFlowRuntime` is the core execution engine.
Responsibilities:
*   Orchestrate node execution
    
*   Resolve connections and ports
    
*   Manage dialog stack
    
*   Track loops and flow state
    
*   Enforce deterministic execution
    
It does **not**:
*   Contain node-specific logic
    
*   Know about UI concerns
    
*   Handle channel rendering
    

* * *

### 🧩 Node Executors

Each node type has a dedicated executor:
*   Implements `INodeExecutor`
    
*   Executes a single node instance
    
*   Returns a `NodeExecutionResult`
    
Executors are:
*   Stateless
    
*   Independently testable
    
*   Replaceable or extendable
    
This makes the runtime **open for extension, closed for modification**.

* * *

### 📡 Dispatcher

The dispatcher:
*   Matches triggers
    
*   Routes execution to the correct flow
    
*   Bridges incoming activities to the runtime
    
It decouples **event sources** from **execution logic**.

* * *

🧠 Memory Model
---------------

Memory is **explicit, scoped, and predictable**.

* * *

### 🗂️ Memory Scopes

Execution context exposes multiple scopes:

#### 🔁 `turn`

*   Lives for a single execution cycle
    
*   Reset after each user interaction
    
*   Ideal for transient data
    

#### 📞 `dialog`

*   Lives for the duration of a dialog
    
*   Preserved across sub-flow calls
    
*   Cleared on `EndDialog`
    

#### 👤 `user`

*   Persists per user
    
*   Suitable for preferences and state
    

#### 💬 `conversation`

*   Shared across all participants
    
*   Persists for the conversation lifetime
    

* * *

### 💾 Persistence Rules

*   Only specific scopes are persisted
    
*   Persistence depends on runtime provider
    
*   In-memory provider is default (MVP)
    
No scope persists unless explicitly allowed.

* * *

### 📦 Serialization

Memory is:
*   JSON-serializable
    
*   Deterministic in shape
    
*   Safe for storage or replay
    
This enables:
*   Stateless hosting
    
*   Resume-after-wait scenarios
    
*   Exported runtimes
    

* * *

🔄 Flow Control Semantics
-------------------------

Flow control nodes influence execution behavior.

* * *

### 🔁 Loops

Loops (`ForEach`, `Repeat`, `ForEachPage`) are tracked via:
*   A loop stack
    
*   Explicit `loop` / `done` ports
    
*   `Break` and `Continue` nodes
    
Nested loops are fully supported.

* * *

### 📚 Dialog Stack

Dialogs use a **call stack model**:
*   `CallDialog` pushes a frame
    
*   Execution switches to sub-flow
    
*   `EndDialog` pops the stack
    
*   Execution resumes at caller
    
This enables:
*   Modular flows
    
*   Reusable sub-flows
    
*   Clear execution boundaries
    

* * *

### 🌿 Parallel Fan-Out (Sequential)

Parallel nodes currently implement a **fan-out / fan-in** model:
*   Branches execute **sequentially**
    
*   Order is deterministic
    
*   All branches complete before continuing
    
True parallel execution is **planned**, not assumed.

* * *

🚨 Error Handling
-----------------

Errors are first-class execution outcomes.

* * *

### ❌ Node Errors

A node may:
*   Return an error result
    
*   Throw an exception
    
Both are captured and logged by the runtime.

* * *

### 🔥 Flow Errors

Flow-level errors occur when:
*   A required executor is missing
    
*   Routing fails
    
*   Execution invariants are violated
    
Such errors terminate execution safely.

* * *

### 🛠️ Recovery Strategies

Current recovery model:
*   Stop execution
    
*   Preserve logs and memory
    
*   Return partial output
    
Advanced recovery strategies are planned.

* * *

🔒 Determinism & Guarantees
---------------------------

The runtime guarantees:
*   Same input → same execution path
    
*   No hidden concurrency
    
*   Explicit state transitions
    
*   No implicit side effects
    
Determinism is a **design principle**, not an optimization.

* * *

⚡ Performance Considerations
----------------------------

Key performance characteristics:
*   O(N) node execution
    
*   No recursive runtime calls
    
*   Minimal allocations per node
    
*   Execution metrics per node available
    
Designed for:
*   Cloud hosting
    
*   Serverless execution
    
*   Embedded runtimes