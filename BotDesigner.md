🎨 Bot Designer — Visual Authoring Experience
=============================================

The **Bot Designer** is the heart of Shaunebu Bot Orchestrator.  
It provides a **visual-first**, schema-driven environment to design, understand, and maintain intelligent conversational workflows.
This section explains how the designer works, how to use it efficiently, and how to scale flows without losing clarity.

* * *

🧱 Canvas Fundamentals
----------------------

The canvas is where flows are authored and visualized.

* * *

### 🔗 Nodes & Ports

*   **Nodes** represent executable units (logic, AI, actions, outputs).
    
*   **Ports** define how execution enters or exits a node.
    
Port types:
*   **Input ports** — where execution arrives
    
*   **Output ports** — where execution continues
    
*   **Named ports** — conditional or branching paths
    
Each node’s ports are defined by its **schema**, not hardcoded UI logic.

* * *

### ➡️ Edges & Connections

Edges define execution paths between nodes.
Key characteristics:
*   Directed (always flow forward)
    
*   Can represent:
    *   Sequential execution
        
    *   Branching
        
    *   Looping
        
*   May be associated with a **named output port**
    
Edges are **data**, not UI artifacts — they are part of the executable model.

* * *

### 🧭 Flow Direction & Semantics

Execution always follows a **top-down logical direction**, regardless of visual layout.
Important notes:
*   Visual placement does **not** affect execution order
    
*   Ports determine semantics, not proximity
    
*   Multiple outgoing edges represent branching
    
The designer enforces **explicit flow clarity**.

* * *

### 🎯 Visual States (Selected, Active, Error)

Nodes and edges reflect runtime and editor states:
*   **Selected** — currently focused in the editor
    
*   **Active** — executing or recently executed
    
*   **Error** — validation or runtime issues detected
    
These visual cues improve readability and debugging.

* * *

🧭 Navigation & Interaction
---------------------------

The designer supports fast navigation and editing, even for large flows.

* * *

### 🖱️ Pan & Zoom

*   Pan the canvas freely
    
*   Zoom in/out for detail or overview
    
*   Fit-to-view supported for quick orientation
    
Designed to handle **large-scale workflows**.

* * *

### 🧲 Multi-Selection

*   Select multiple nodes at once
    
*   Move groups together
    
*   Prepare for bulk operations (future)
    
Multi-selection is essential for refactoring flows.

* * *

### 📦 Drag & Drop

*   Drag nodes from the palette to the canvas
    
*   Reposition nodes freely
    
*   Reconnect edges interactively
    
All drag actions preserve model integrity.

* * *

### ⌨️ Keyboard Shortcuts

Common shortcuts include:
*   Delete selected nodes
    
*   Save flow
    
*   Undo / redo (planned)
    
*   Quick navigation (planned)
    
Keyboard usage is encouraged for power users.

* * *

🧩 Node Palette
---------------

The Node Palette is the entry point for all available building blocks.

* * *

### 🗂️ Category System

Nodes are grouped by intent, not implementation:
*   Triggers
    
*   AI
    
*   Actions
    
*   Logic
    
*   Outputs
    
This keeps discovery intuitive, even as the node set grows.

* * *

### 🔍 Search & Filtering

*   Search nodes by name or description
    
*   Results update instantly
    
*   Categories auto-expand when filtered
    
Designed for fast node discovery.

* * *

### ⚙️ Static vs Dynamic Nodes

*   **Static nodes** — built-in, always available
    
*   **Dynamic nodes** — loaded via schemas or plugins
    
The palette is **schema-driven**, not hardcoded.

* * *

### 🛒 Marketplace Nodes

Marketplace nodes allow extending the system without modifying core code.
*   Installable via JSON schemas
    
*   Future: install/update/search UI
    
This enables a plugin-based ecosystem.

* * *

🔍 Inspector Panels
-------------------

The Inspector provides detailed configuration and validation.

* * *

### 🧩 Properties Panel

*   Primary configuration UI
    
*   Driven by node schema
    
*   Supports expressions and literals
    
Changes are applied immediately.

* * *

### 🧮 Expression Editor

*   Supports `memory.*` expressions
    
*   Auto-complete and validation
    
*   Used across conditions, prompts, and actions
    
Expressions are evaluated at runtime.

* * *

### 🧾 Raw JSON View

*   Direct access to node definition
    
*   Useful for advanced users
    
*   Enables fine-grained control
    
This view reflects the **source of truth**.

* * *

### ⚠️ Validation Feedback

The inspector highlights:
*   Missing required fields
    
*   Invalid expressions
    
*   Structural issues
    
Validation prevents invalid flows from executing.

* * *

🗂️ File Explorer
-----------------

The File Explorer manages flows and project structure.

* * *

### 📁 Managing Flows

*   Create, rename, delete flows
    
*   Switch between flows
    
*   Maintain multiple bots or subflows
    
Flows are first-class entities.

* * *

### 🏷️ Naming & Organization

Good naming conventions improve maintainability:
*   Use descriptive flow names
    
*   Avoid generic labels
    
*   Reflect intent, not implementation
    

* * *

### 🧭 Composer-Style Navigation

Inspired by Bot Framework Composer:
*   Clear hierarchy
    
*   Familiar UX patterns
    
*   Optimized for complex projects
    

* * *

🧠 UX Patterns & Best Practices
-------------------------------

Designing readable flows is critical.

* * *

### 👁️ Readability

*   Avoid crossing edges
    
*   Keep linear paths aligned
    
*   Group related logic visually
    
A readable flow is a debuggable flow.

* * *

### 🛠️ Maintainability

*   Prefer smaller flows over monoliths
    
*   Use Call Dialog for reuse
    
*   Isolate AI logic from control logic
    
Design for change.

* * *

### 🗺️ Large Flow Management

For large bots:
*   Break logic into subflows
    
*   Use clear branching
    
*   Document intent via naming
    
The designer scales best with modular design.

* * *

⚠️ Known Limitations
--------------------

Current limitations to be aware of:
*   No true parallel execution (sequential fan-out only)
    
*   Undo/Redo partially implemented
    
*   Auto-layout is planned, not default
    
*   Collaboration is single-user only
    
These limitations are addressed in the roadmap.