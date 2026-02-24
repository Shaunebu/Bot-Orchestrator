🚀 Getting Started — Shaunebu Bot Orchestrator
==============================================

* * *

🛠️ Installation & Setup
------------------------

This section helps you prepare your environment and understand the basic configuration required to start working with Shaunebu Bot Orchestrator.

* * *

### 📋 Requirements

Before you begin, ensure you have the following:
*   **Operating System**
    *   Windows 10/11 (primary)
        
    *   macOS / Linux (runtime support planned)
        
*   **Development Stack**
    *   .NET 8+ (Runtime & Host)
        
    *   Node.js 18+ (Designer UI)
        
    *   Modern browser (Edge, Chrome)
        
*   **Optional**
    *   Docker (for future exporters)
        
    *   Azure account (for deployment scenarios)
        

* * *

### 💻 Local Environment

A typical local setup consists of two components:
1.  **Designer (Frontend)**
    *   Visual canvas
        
    *   Node palette
        
    *   Inspector & debugger
        
2.  **Runtime Host (Backend)**
    *   Flow execution engine
        
    *   Node executors
        
    *   Memory and logging
        
Both can run locally for development and testing.

> 💡 The designer and runtime are intentionally decoupled to support future deployment and export scenarios.

* * *

### ⚙️ Configuration Overview

Core configuration concepts include:
*   **Flow definitions** (JSON-based)
    
*   **Node schemas** (schema-driven behavior)
    
*   **Runtime settings**
    *   AI providers
        
    *   Memory providers
        
    *   Logging
        
At this stage, defaults are sufficient to get started.

* * *

🧩 Creating Your First Bot
--------------------------

This walkthrough demonstrates the minimum steps required to build and run a bot.

* * *

### 🧱 Creating a Flow

A **flow** is the executable definition of your bot logic.
Steps:
1.  Open the Designer
    
2.  Create a new flow
    
3.  Name your flow
    
Each flow represents a **self-contained orchestration unit**.

* * *

### ⚡ Adding a Trigger

Triggers define **when a flow starts**.
Examples:
*   On message received
    
*   On conversation start
    
*   On condition
    
Steps:
1.  Drag a **Trigger** node to the canvas
    
2.  Configure its trigger type
    
3.  Connect it to the next node
    

* * *

### 💬 Adding a Response

Responses define what the bot sends back to the user.
Steps:
1.  Add a **Response** node
    
2.  Set the response text
    
3.  Connect it from the Trigger
    
At this point, your flow is already executable.

* * *

### ▶️ Running the Bot

To test your bot:
1.  Start the runtime host
    
2.  Open WebChat
    
3.  Send a message
    
You should see:
*   The Trigger fire
    
*   The Response execute
    
*   Output rendered in the chat
    

* * *

🧭 Understanding the UI at a Glance
-----------------------------------

The Designer UI is composed of several core areas.

* * *

### 🎨 Canvas

*   Visual workspace
    
*   Drag & drop nodes
    
*   Connect flows using edges
    
*   Pan, zoom, and arrange logic visually
    

* * *

### 🧩 Node Palette

*   Categorized list of available nodes
    
*   Searchable
    
*   Schema-driven
    
Nodes are grouped by intent:
*   Triggers
    
*   AI
    
*   Actions
    
*   Logic
    
*   Outputs
    

* * *

### 🔍 Inspector

The Inspector shows detailed information for the selected node.
Includes:
*   Properties editor
    
*   Raw JSON view
    
*   Validation feedback
    
This is where behavior is configured.

* * *

### 🐞 Debugger

The Debugger allows you to:
*   Step through execution
    
*   View logs
    
*   Inspect memory
    
*   Understand flow behavior
    
It is designed to make execution **observable and explainable**.

* * *

🧠 First Concepts Explained
---------------------------

Understanding these concepts is critical before building complex bots.

* * *

### 🔁 What Is a Flow

A **flow** is a directed graph of nodes and edges.
*   It represents logic, not UI
    
*   It is executable
    
*   It is exportable
    
Flows are the core unit of orchestration.

* * *

### 🧱 What Is a Node

A **node** is a unit of behavior.
Examples:
*   Trigger
    
*   Decision
    
*   AI Prompt
    
*   HTTP Action
    
*   Response
    
Each node:
*   Has inputs and outputs
    
*   Is defined by a schema
    
*   Has a runtime executor
    

* * *

### ➡️ What Is an Edge

An **edge** connects two nodes.
*   Defines execution order
    
*   Can be conditional
    
*   Can represent branching or looping
    
Edges control flow direction.

* * *

### 🧠 What Is Memory

Memory stores execution state.
Common scopes:
*   `turn` — current interaction
    
*   `conversation` — session-level
    
*   `user` — persistent user data
    
Memory is accessible via expressions and nodes.

* * *

🛣️ Next Learning Paths
-----------------------

Depending on your goals, continue with one of the following paths:

* * *

### 💬 Conversational Bots

*   Focus on dialogue
    
*   Triggers, Decisions, Responses
    
*   State-driven conversations
    

* * *

### 🤖 AI-Driven Bots

*   AI Prompt nodes
    
*   Tool calling
    
*   Structured outputs
    
*   Safety and guardrails
    

* * *

### 🔗 Backend-Integrated Bots

*   HTTP actions
    
*   External services
    
*   Export to APIs or functions