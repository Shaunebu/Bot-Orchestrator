🐞 Debugging & Testing — Understand, Inspect, and Trust Your Bots
=================================================================

This section explains how to **observe**, **debug**, and **test** bot executions in Shaunebu Bot Orchestrator.  
The platform is designed so that **every execution is explainable**, reproducible, and auditable.

* * *

🧭 Debugger Overview
--------------------

The Debugger provides **real-time visibility** into how a flow executes.
Key goals:
*   Understand _what happened_
    
*   Understand _why it happened_
    
*   Understand _what data changed_
    
The debugger is **execution-driven**, not UI-driven.

* * *

### 🧠 What the Debugger Shows

During execution, the debugger exposes:
*   Active node
    
*   Execution order
    
*   Node execution duration
    
*   Memory changes
    
*   Logs emitted by nodes
    
Everything you see corresponds **directly to runtime behavior**.

* * *

🧾 Execution Logs
-----------------

Execution logs are the primary diagnostic tool.

* * *

### 📜 Log Characteristics

Logs are:
*   Emitted by the runtime and node executors
    
*   Timestamped implicitly by execution order
    
*   Ordered deterministically
    
Logs are never inferred or simulated.

* * *

### 🔍 What Gets Logged

Examples of logged events:
*   Trigger evaluation results
    
*   Node execution start and end
    
*   Branch execution (Parallel fan-out)
    
*   Expression evaluation outcomes
    
*   Errors and early termination
    
Logs are designed to answer:

> _“Why did the flow go here?”_

* * *

⏭️ Step-By-Step Execution
-------------------------

Execution is inherently step-by-step.
Each node:
1.  Starts execution
    
2.  Produces logs
    
3.  Mutates memory (if applicable)
    
4.  Selects an output port
    
5.  Ends execution
    
This makes stepping trivial:
*   One node = one step
    
*   One decision = one port
    
There is no hidden background execution.

* * *

🧠 Inspecting Memory
--------------------

Memory inspection is a core debugging feature.

* * *

### 🗂️ Memory Scopes in Debugger

The debugger shows all scopes:
*   `turn`
    
*   `dialog`
    
*   `user`
    
*   `conversation`
    
Each scope is:
*   Readable
    
*   Editable (when allowed)
    
*   Scoped correctly to execution
    

* * *

### 🔄 Watching Memory Changes

You can:
*   See values before execution
    
*   Observe changes after each node
    
*   Identify where data was introduced or overwritten
    
This makes data flow **traceable**, not magical.

* * *

🧪 Testing Strategies
---------------------

Testing in Shaunebu Bot Orchestrator is layered.

* * *

### 🧍 Manual Testing

Manual testing is ideal for:
*   Flow validation
    
*   UX verification
    
*   Early prototyping
    
Using WebChat or channel simulators, you can:
*   Send inputs
    
*   Observe outputs
    
*   Inspect memory and logs
    

* * *

### 🧪 Flow-Level Testing

Flow-level testing focuses on logic correctness.
Recommended approach:
*   Design flows with deterministic branches
    
*   Use explicit Decision nodes
    
*   Avoid side effects in early nodes
    
This allows:
*   Predictable execution paths
    
*   Repeatable test runs
    

* * *

### 🧩 Mocked Actions

Actions (HTTP, external calls, AI prompts) can be mocked.
Benefits:
*   No external dependencies
    
*   Faster test cycles
    
*   Safer iteration
    
Mocking is especially useful for:
*   HTTP Action nodes
    
*   AI Prompt simulations
    
*   Backend-dependent logic
    

* * *

🚨 Common Failure Scenarios
---------------------------

Most issues fall into known categories.

* * *

### ❌ Trigger Never Fires

Causes:
*   Trigger condition evaluates to false
    
*   Activity type mismatch
    
*   Incorrect trigger configuration
    
Solution:
*   Inspect trigger logs
    
*   Validate activity payload
    

* * *

### 🔀 Wrong Branch Taken

Causes:
*   Expression logic error
    
*   Unexpected memory values
    
*   Type coercion issues
    
Solution:
*   Inspect Decision node logs
    
*   Verify memory state before evaluation
    

* * *

### 🧠 Missing or Overwritten Memory

Causes:
*   Writing to wrong scope
    
*   Name collisions
    
*   Assumptions about persistence
    
Solution:
*   Inspect scope boundaries
    
*   Use explicit memory paths
    

* * *

### ⏸️ Execution Stops Unexpectedly

Causes:
*   Node returns `Waiting`
    
*   Dialog not resumed
    
*   No valid outgoing connection
    
Solution:
*   Check execution status
    
*   Verify flow connections visually
    

* * *

### 🔥 Runtime Error

Causes:
*   Missing node executor
    
*   Invalid configuration
    
*   Unsupported execution pattern
    
Solution:
*   Check runtime logs
    
*   Validate node schemas