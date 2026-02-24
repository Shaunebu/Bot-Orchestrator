🧩 Nodes Reference — Execution Building Blocks
==============================================

Nodes are the fundamental execution units in **Shaunebu Bot Orchestrator**.  
Each node represents a **well-defined, schema-driven operation** that participates in the deterministic execution of a flow.
This section documents **how nodes work**, **how they are classified**, and **how to use each node type correctly**.

* * *

🧠 Node System Overview
-----------------------

The node system is fully **schema-driven** and runtime-agnostic.

* * *

### 📐 Node Schema Anatomy

Each node is defined by a schema that includes:
*   **Type** — unique identifier (`Decision`, `Response`, `Parallel`, etc.)
    
*   **Category** — how it appears in the Node Palette
    
*   **Inputs** — accepted flow entry points
    
*   **Outputs** — possible execution exits
    
*   **Properties** — configurable parameters
    
*   **Defaults** — initial values
    
*   **UI metadata** — icon, color, grouping
    
*   **Execution contract** — runtime behavior
    
The schema is the **single source of truth**.

* * *

### 🔗 Inputs & Outputs

*   Inputs define **where execution may enter**
    
*   Outputs define **how execution may continue**
    
*   Outputs can be:
    *   Single (`next`, `out`)
        
    *   Named (`true`, `false`, `A`, `B`, etc.)
        
Execution follows **ports**, not visual layout.

* * *

### ⚙️ Properties & Defaults

*   Properties store node configuration
    
*   Defaults are applied on node creation
    
*   Values may be:
    *   Static literals
        
    *   Expressions (`memory.*`)
        
    *   JSON payloads
        
All properties are validated against the schema.

* * *

### 📜 Execution Contract

Every node executor follows a strict contract:
*   Executes synchronously or asynchronously
    
*   Returns a `NodeExecutionResult`
    
*   Declares:
    *   Status (Success, Error, Waiting, Stop)
        
    *   Next port or next node
        
*   Must not mutate flow structure
    
This guarantees **predictable execution**.

* * *

⚡ Triggers
----------

Triggers define **how a flow starts**.

* * *

### 🔔 Trigger Node

*   Entry point of a flow
    
*   Evaluated before any other node
    
*   Only one trigger fires per execution cycle
    
Triggers do not receive input ports.

* * *

### 🧩 Trigger Types

Common trigger types include:

#### 📨 OnMessageActivity

*   Fires when a message is received
    
*   Optional condition expression
    

#### 🧠 OnIntentRecognized

*   Fires when NLP intent is detected
    
*   Supports confidence thresholds
    

#### 🔍 OnCondition

*   Fires when a memory-based condition is true
    

#### 🚀 OnStartConversation

*   Fires only once per conversation start
    

#### ➕ Others

*   Event-based triggers
    
*   Webhook triggers
    
*   Cron/scheduled triggers (planned)
    

* * *

### ✅ Trigger Best Practices

*   Keep trigger conditions simple
    
*   Avoid heavy logic in triggers
    
*   Delegate processing to downstream nodes
    
Triggers decide **when**, not **how**.

* * *

🤖 AI Nodes
-----------

AI nodes integrate Large Language Models into flows.

* * *

### 🧠 AI Prompt

*   Core LLM interaction node
    
*   Supports:
    *   System prompt
        
    *   User prompt
        
    *   Few-shot examples
        
    *   Tools (function calling)
        

* * *

### 👤 User Prompt

*   Specialized prompt sourced from user input
    
*   Useful for conversational patterns
    

* * *

### 🧪 Prompt Modes (Simple vs Advanced)

*   **Simple mode** — minimal configuration
    
*   **Advanced mode** — full control over provider, parameters, tools
    
Schemas adapt dynamically based on mode.

* * *

### 🌊 Streaming Behavior

*   Optional streaming support
    
*   Enables token-by-token rendering
    
*   Requires channel compatibility
    

* * *

### 💰 Cost & Token Considerations

AI nodes may expose:
*   Estimated token usage
    
*   Provider-specific constraints
    
*   Cost awareness (display-only)
    
Runtime enforces no billing by default.

* * *

🧠 Logic Nodes
--------------

Logic nodes control decision-making.

* * *

### 🔀 Decision

*   Evaluates a boolean expression
    
*   Routes execution via `true` / `false` ports
    
Used for conditional branching.

* * *

### 🧭 Switch

*   Multi-branch decision node
    
*   Routes execution based on matching cases
    
*   More expressive than Decision
    

* * *

### 🧮 Expressions & Conditions

Expressions:
*   Use `memory.*` paths
    
*   Support logical and comparison operators
    
*   Evaluated deterministically
    
Expressions never mutate state.

* * *

⚙️ Action Nodes
---------------

Action nodes perform **side effects**.

* * *

### 🌐 HTTP Action

*   Calls external APIs
    
*   Supports headers, body, method
    
*   Can store response in memory
    
Simulated or real execution depending on runtime.

* * *

### 🧠 Memory Operations

*   Read from memory
    
*   Write to memory
    
*   Scope-aware (`turn`, `dialog`, `user`, `conversation`)
    
Memory is explicit and observable.

* * *

### 🏷️ Set Property

*   Writes a value to memory
    
*   Supports expressions
    
*   Deterministic assignment
    
Used to prepare data for later nodes.

* * *

### ⏱️ Delay

*   Pauses execution for a fixed duration
    
*   Non-blocking at runtime level
    
Useful for pacing and UX flows.

* * *

### 🧩 Custom Actions

*   Implemented via Skill SDK
    
*   Schema-defined
    
*   Runtime-executed
    
Allows full extensibility.

* * *

🔄 Flow Control Nodes
---------------------

These nodes alter execution flow mechanics.

* * *

### 🌿 Parallel

Runs multiple branches from a single node.

#### 🔀 Fan-Out Model (MVP)

*   Branches execute **sequentially**
    
*   Order is deterministic
    
*   No true concurrency yet
    

#### ⏱️ Execution Order

*   Branches execute in declaration order
    
*   All branches complete before `next`
    

#### ⚠️ Known Constraints

*   No `Waiting` inside branches (MVP)
    
*   No shared branch synchronization
    
*   True DAG execution planned
    

* * *

### 🔁 ForEach

*   Iterates over a collection
    
*   Exposes current item to memory
    
*   Supports `loop` and `done` ports
    

* * *

### 📄 ForEach Page

*   Iterates paged collections
    
*   Useful for APIs with pagination
    
*   Page-aware looping semantics
    

* * *

### 🔂 Repeat

*   Loops while a condition remains true
    
*   Condition re-evaluated each iteration
    

* * *

### ⛔ Break

*   Exits the nearest active loop
    
*   Transfers execution to loop’s `done` port
    

* * *

### ▶️ Continue

*   Skips remaining loop body
    
*   Jumps back to loop entry
    

* * *

📦 Dialog Nodes
---------------

Dialog nodes manage **sub-flow execution**.

* * *

### 📞 Call Dialog

Invokes another flow as a sub-dialog.

#### 🔁 Sub-Flow Invocation

*   Switches execution context
    
*   Passes memory and state
    
*   Preserves call hierarchy
    

#### 🧠 Stack Behavior

*   Call stack maintained
    
*   Nested dialogs supported
    
Used for modularization.

* * *

### 🔚 End Dialog

Terminates the current dialog.

#### 🔙 Returning Control

*   Returns execution to caller flow
    
*   Resumes after Call Dialog
    

#### 🛑 Flow Termination

*   If no caller exists, ends execution
    

* * *

📤 Output Nodes
---------------

Output nodes produce user-visible results.

* * *

### 💬 Response

*   Sends text or structured messages
    
*   Channel-aware rendering
    
*   May optionally enter Waiting state
    
Primary conversational output.

* * *

### 📦 Output

*   Emits structured payloads
    
*   Used for integrations or APIs
    
*   Not always user-visible
    

* * *

### 🎨 Channel Rendering Rules

Rendering depends on channel:
*   WebChat
    
*   Messaging platforms
    
*   Custom hosts
    
Nodes emit **intent**, channels decide **presentation**.