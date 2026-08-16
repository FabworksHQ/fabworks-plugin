# Fabworks MCP plugin

[![skills.sh](https://skills.sh/b/FabworksHQ/fabworks-plugin)](https://skills.sh/FabworksHQ/fabworks-plugin)

[Fabworks](https://www.fabworks.com) is an online laser cutting service: upload a STEP file, get a price, and order custom sheet metal and tube parts. This plugin connects Claude Code, Codex, Cursor, and other MCP-capable coding agents to the Fabworks remote Model Context Protocol (MCP) server. One Fabworks Agent Skill covers quoting, materials, bending, hole operations, finishes, and DFM.

## What it does

- Finds exact Fabworks materials, tube profiles, thicknesses, and finishes.
- Uploads STEP files through signed URLs so CAD file bytes stay out of the agent context.
- Creates and updates quotes for flat sheet, bent sheet, and tube laser cutting.
- Returns quote pricing, part configuration, DFM results, and checkout links.
- Authenticates with browser-based OAuth or a Fabworks API key.

## Install

Install the MCP configuration and the Fabworks Agent Skill:

```bash
npx plugins add FabworksHQ/fabworks-plugin
```

Install the Fabworks Agent Skill by itself:

```bash
npx skills add FabworksHQ/fabworks-plugin --skill fabworks
```

The remote MCP server is available at `https://api.fabworks.com/mcp`. The connection starts a browser-based OAuth flow.

## Included Agent Skill

- [`fabworks`](https://github.com/FabworksHQ/fabworks-plugin/tree/main/skills/fabworks): Creates and manages quotes, interprets MCP results, and answers Fabworks fabrication questions. It loads focused references for services, laser cutting, bending, hole operations, materials, finishes, and DFM only when they are needed.

Read the [Fabworks MCP documentation](https://www.fabworks.com/resources/developers/mcp) for setup instructions, available tools, and example quote requests.
