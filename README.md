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


🔍 Testing Locally with MCP Inspector
To test your custom server without configuring a massive client application, use the official browser-based developer suite. Run this command directly from your terminal workspace:

Bash
npx @modelcontextprotocol/inspector node index.mjs
Open the local link outputted in your console (e.g., http://localhost:3000).

Verify the status indicator turns green (Connected).

Navigate to the Tools tab in the dashboard panel.

Select calculate_efficiency, pass your test payload arguments, and hit Call Tool to see the local server execute in real-time.
