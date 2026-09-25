# Fabworks MCP plugin

[Fabworks](https://www.fabworks.com) is an online laser cutting service: upload a STEP file, get a price, and order custom sheet metal and tube parts. This plugin connects Claude Code, Codex, Cursor, and other MCP-capable coding agents to the Fabworks remote Model Context Protocol (MCP) server.

## What it does

- Finds exact Fabworks materials, tube profiles, thicknesses, and finishes.
- Uploads STEP files through signed URLs so CAD file bytes stay out of the agent context.
- Creates and updates quotes for flat sheet, bent sheet, and tube laser cutting.
- Returns quote pricing, part configuration, DFM results, bend data, delivery options, and checkout links.
- Authenticates with browser-based OAuth or a Fabworks API key.

## Install

```bash
npx plugins add FabworksHQ/fabworks-plugin
```

The remote MCP server is available at `https://api.fabworks.com/mcp`. The connection starts a browser-based OAuth flow.

## Agent Guidance

The server hands agents the Fabworks playbook: the quoting workflow, how to read DFM and bend results, and limits for laser cutting, bending, hole operations, materials, and finishes. Agents load it with the `get_agent_guidance` tool. People can read it at [fabworks.com/resources/developers/agent-guidance](https://www.fabworks.com/resources/developers/agent-guidance).

Read the [Fabworks MCP documentation](https://www.fabworks.com/resources/developers/mcp) for setup instructions, available tools, and example quote requests.
