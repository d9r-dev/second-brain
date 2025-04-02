---
title: Model Context Protocol (MCP)
draft: false
publish: true
tags:
  - 🌲
  - artificial-intelligence
  - large-language-models
date: 2025-04-02
---
MCP is an open standard for AI ([[Artificial Intelligence]]) models to connect to many different apps and data sources in a consistent way. 

This is the **language and rules** that the clients and servers use to communicate. It defines things like message formats, how a server advertises its available commands, how an AI asks a question or issues a command, and how results are returned. The protocol is transport-agnostic: it can work over **HTTP/WebSockets for remote or standalone servers, or even standard IO streams (stdin/stdout) for local integrations**. The content of the messages might be JSON or another structured schema (the spec uses JSON Schema for definitions). Essentially, the protocol ensures that whether an AI is talking to a design tool or a database, the **handshake and query format** are consistent. This consistency is why an AI can switch from one MCP server to another without custom coding – the **“grammar” of interaction remains the same**.

For example, with MCP an AI model could **fetch information from a database, edit a design in Figma, or control a music app** – all by sending natural-language instructions through a standardized interface.

MCP follows a client-server architecture. 

- MCP Servers: lightweight adapters that expose an applications's functionality in a standardized way. It knows how to take a natural-language request and perform the equivalent action in the app
	- Tool Discovery: which actions/capabilities the application offers
	- Command Parsing: They interpret from the AI incoming instructions for exact commands or API calls
	- Response Formatting: Format the Output of the Application so that the AI understands it
	- Error Handling: Catch exceptions and respond appropriately to the AI
- MCP Clients: 
	- maintains 1:1 connection to server
	- AI connects through the MCP Client to the MCP Server
- Services:
	- the actual applications the AI interfaces with

## Links

[# MCP: What It Is and Why It Matters](https://addyo.substack.com/p/mcp-what-it-is-and-why-it-matters?utm_source=fullstackbulletin.com&utm_medium=newsletter&utm_campaign=fullstackBulletin-13-2025&utm_content=title)