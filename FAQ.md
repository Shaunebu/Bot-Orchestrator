❓ FAQ & Troubleshooting — Common Questions and Practical Solutions
==================================================================

This section answers the most common questions about Shaunebu Bot Orchestrator and provides guidance for diagnosing and resolving typical issues.
It is intended as a **first stop for problem-solving** before diving into logs or internal documentation.

* * *

💡 Conceptual Questions
-----------------------

### ❓ Is Shaunebu Bot Orchestrator a chatbot framework?

Not exactly.
Shaunebu Bot Orchestrator is a **visual orchestration platform** for conversational logic.  
It focuses on **flow design, execution semantics, and exportability**, not on UI or channel lock-in.

* * *

### ❓ Do I need to write code to use it?

No.
The platform is **visual-first and code-optional**:
*   Most bots can be built entirely using the designer
    
*   Code is only required for advanced extensibility (custom nodes, skills, exporters)
    

* * *

### ❓ Is this meant for AI-only bots?

No.
It supports:
*   Rule-based bots
    
*   AI-assisted bots
    
*   Hybrid conversational systems
    
*   Backend-driven workflows
    
AI is **a capability**, not a requirement.

* * *

### ❓ What is the difference between a Flow and a Dialog?

*   A **Flow** is a full execution graph
    
*   A **Dialog** is a reusable sub-flow invoked from another flow
    
Dialogs enable modular design and reuse without duplicating logic.

* * *

⚙️ Runtime Issues
-----------------

### ❌ My flow starts but nothing happens

Check:
*   The Trigger configuration
    
*   Trigger conditions (expressions may evaluate to false)
    
*   That the trigger output is connected to the next node
    
Use the Debugger to confirm trigger activation.

* * *

### ❌ A node executes but does not route correctly

Common causes:
*   Missing or incorrect port connections
    
*   Incorrect `nextPortId` returned by the node executor
    
*   Mismatched port IDs between schema and flow JSON
    
Validate port names carefully.

* * *

### ❌ Parallel node executes but responses appear at the end

This is expected behavior.
Current Parallel execution uses a **sequential fan-out model**:
*   Branches run one after another
    
*   Output is flushed after execution completes
    
True asynchronous streaming is planned for future versions.

* * *

🚦 Performance Issues
---------------------

### 🐢 My flow feels slow

Check for:
*   Long Delay nodes
    
*   External HTTP calls
    
*   Large AI prompts or token limits
    
Use execution logs to identify slow nodes.

* * *

### 🧠 Memory grows unexpectedly

Ensure:
*   Large objects are not stored in long-lived scopes (user, conversation)
    
*   Temporary data uses the `turn` scope
    
*   Memory keys are overwritten intentionally
    
Memory scope discipline is essential for performance.

* * *

⚠️ Known Limitations
--------------------

The following limitations are **by design or temporarily constrained**:
*   Parallel branches are sequential (MVP)
    
*   Waiting states inside Parallel branches are not supported
    
*   No real-time streaming per branch yet
    
*   No distributed memory provider by default (InMemory only)
    
These are tracked and documented in the roadmap.

* * *

🐞 Reporting Issues
-------------------

If you encounter a bug or unexpected behavior:

### 📋 Before reporting

Collect:
*   Flow JSON
    
*   Execution logs
    
*   Runtime version
    
*   Clear reproduction steps
    

* * *

### 📣 Where to report

Issues should be reported through:
*   The official issue tracker
   
    
Clear, reproducible reports receive faster resolution.