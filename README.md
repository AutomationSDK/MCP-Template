# MCP-Template
A minimal, zero-fluff Node.js boilerplate for building a local Model Context Protocol (MCP) server. Connect LLMs securely to your local file systems, tools, and databases with no subscription fees.

# 🚀 5-Minute Local MCP Server Template

Stop manually copy-pasting data between your AI workflows and your tools. You are wasting time, introducing friction, and missing the core benefit of autonomous software architectures. 

This repository provides a minimal, production-ready boilerplate to spin up a local **Model Context Protocol (MCP)** server using Node.js. Give your AI agents structural access to act directly inside your local environment, completely free, private, and secure.

---

## 🛠️ Tech Stack & Prerequisites

- **Runtime:** Node.js (v18 or higher recommended)
- **Protocol:** Official `@modelcontextprotocol/sdk`
- **Transport:** Standard Input/Output (`stdio`)

---

## 🚀 Quick Start Guide

### 1. Initialize the Workspace
Open your terminal (use **Command Prompt** if you are on Windows to bypass PowerShell script execution restrictions) and run:

npm init -y

2. Install the MCP SDK
Install the official Model Context Protocol developer kit:

Bash
npm install @modelcontextprotocol/sdk
3. Create the Server Core (index.mjs)
Create a file named exactly index.mjs. Using the .mjs extension forces Node.js to recognize modern ES module imports cleanly, bypassing configuration conflicts.

Paste the following logic into index.mjs:

import { Server } from "@modelcontextprotocol/sdk/server/index.js";
import { StdioServerTransport } from "@modelcontextprotocol/sdk/server/stdio.js";
import {
  CallToolRequestSchema,
  ListToolsRequestSchema,
} from "@modelcontextprotocol/sdk/types.js";

// Initialize the local MCP Server
const server = new Server(
  {
    name: "automation-hub-server",
    version: "1.0.0",
  },
  {
    capabilities: {
      tools: {}, 
    },
  }
);

// Define your custom tool schema (The "Cognition Layer")
server.setRequestHandler(ListToolsRequestSchema, async () => {
  return {
    tools: [
      {
        name: "calculate_efficiency",
        description: "Calculates time saved by automating a repetitive task.",
        inputSchema: {
          type: "object",
          properties: {
            taskName: { type: "string", description: "Name of the manual task" },
            manualMinutes: { type: "number", description: "Minutes spent manually per day" },
            automatedMinutes: { type: "number", description: "Minutes spent after automation" },
          },
          required: ["taskName", "manualMinutes", "automatedMinutes"],
        },
      },
    ],
  };
});

// Handle the tool execution logic
server.setRequestHandler(CallToolRequestSchema, async (request) => {
  if (request.params.name === "calculate_efficiency") {
    const { taskName, manualMinutes, automatedMinutes } = request.params.arguments;
    
    const dailySaved = manualMinutes - automatedMinutes;
    const yearlySavedHours = Math.round((dailySaved * 365) / 60);

    return {
      content: [
        {
          type: "text",
          text: `📊 Automation Report for '${taskName}':\n` +
                `- Time saved per day: ${dailySaved} minutes.\n` +
                `- Total efficiency gained: ${yearlySavedHours} hours saved per year! 🚀`,
        },
      ],
    };
  }

  throw new Error(`Tool not found: ${request.params.name}`);
});

// Boot up the server over stdio transport
async function runServer() {
  const transport = new StdioServerTransport();
  await server.connect(transport);
  console.error("MCP Server running smoothly on stdio!");
}

runServer().catch((error) => {
  console.error("Fatal error running MCP server:", error);
  process.exit(1);
});

🔍 Testing Locally with MCP Inspector
To test your custom server without configuring a massive client application, use the official browser-based developer suite. Run this command directly from your terminal workspace:

Bash
npx @modelcontextprotocol/inspector node index.mjs
Open the local link outputted in your console (e.g., http://localhost:3000).

Verify the status indicator turns green (Connected).

Navigate to the Tools tab in the dashboard panel.

Select calculate_efficiency, pass your test payload arguments, and hit Call Tool to see the local server execute in real-time.
