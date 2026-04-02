This system demonstrates a full-stack AI-powered warehouse automation solution integrating structured data (Supabase), workflow automation (n8n), and intelligent querying via MCP and RAG

# The-Intelligent-Warehouse-Inventory-Orchestrator

## 🎨 Frontend (Warehouse Dashboard + AI Chat)

### Overview

The frontend was built using Lovable, a vibecoding platform for rapid UI development.
It provides a clean and responsive dashboard for warehouse operations and an AI chat interface.

Live App:
https://pack-pilot-ai.lovable.app

---

## ⚙️ Features

### 1. Inventory Operations

* Users can perform:

  * Inbound (add stock)
  * Outbound (remove stock)
* Sends requests to n8n backend via webhook:

  * `/inventory-operation`

---

### 2. Inventory Health Check

* Fetches items where:
  stock_level < reorder_point
* Displays results in a table
* Connected to:

  * `/inventory-health`

---

### 3. AI Chat Interface

* Users can ask:

  * Inventory questions
  * Logs queries
  * Product manual questions (RAG)
* Connected to:

  * `/ai-agent-advanced`

---

## 🔌 API Integration

The frontend communicates with n8n via HTTP requests:

### Inventory Operation

POST /webhook/inventory-operation

### Inventory Health

GET /webhook/inventory-health

### AI Agent

POST /webhook/ai-agent-advanced

All requests are handled using JavaScript fetch API within the Lovable environment.

---

## 💻 Localhost Deployment Guide

Since Lovable is a hosted platform, local deployment is simulated by recreating the frontend logic in a local environment.

### Steps:

1. Create a simple HTML file (index.html)

2. Add JavaScript logic for API calls:

```html
<script>
async function sendMessage() {
  const input = document.getElementById("chatInput").value;

  const res = await fetch("http://localhost:5678/webhook/ai-agent-advanced", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify({ message: input })
  });

  const data = await res.json();
  console.log(data);
}
</script>
```

3. Run n8n locally:

```
n8n start
```

4. Open index.html in browser

---

## 🧠 Design Decisions

* Used Lovable for rapid UI development and clean UX
* Separated frontend and backend via API-first architecture
* Ensured real-time communication with n8n workflows
* Focused on usability and clarity for warehouse staff

---

## 🚧 Future Improvements

* Add authentication for user roles
* Improve UI state management
* Add real-time updates (WebSockets)
* Deploy custom frontend with React/Next.js
