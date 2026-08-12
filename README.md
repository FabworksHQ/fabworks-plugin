# Fabworks MCP plugin

[![skills.sh](https://skills.sh/b/FabworksHQ/fabworks-plugin)](https://skills.sh/FabworksHQ/fabworks-plugin)

[Fabworks](https://www.fabworks.com) is an online laser cutting service: upload a STEP file, get a price, order custom sheet metal and tube parts. This plugin connects Claude Code, Codex, Cursor, and other MCP-capable coding agents to the Fabworks remote Model Context Protocol (MCP) server so they can create quotes, review pricing and DFM results, update quote parts, and check order status.

## What it does

- Finds exact Fabworks materials, tube profiles, thicknesses, and finishes.
- Uploads STEP files through signed URLs so CAD file bytes stay out of the agent context.
- Creates and updates quotes for flat sheet, bent sheet, and tube laser cutting.
- Returns quote pricing, part configuration, DFM results, and checkout links.
- Authenticates with browser-based OAuth or a Fabworks API key.

## Install

Install the MCP configuration and both Fabworks Agent Skills:

```bash
npx plugins add FabworksHQ/fabworks-plugin
```

Install an individual Agent Skill:

```bash
npx skills add FabworksHQ/fabworks-plugin --skill quote-with-fabworks
npx skills add FabworksHQ/fabworks-plugin --skill understand-fabrication
```

The remote MCP server is available at `https://api.fabworks.com/mcp`. The connection starts a browser-based OAuth flow.

## Included Agent Skills

- [`quote-with-fabworks`](https://www.skills.sh/fabworkshq/fabworks-plugin/quote-with-fabworks): Runs the full quoting workflow: resolve exact catalog IDs, upload STEP files through signed URLs, create and update quotes, and handle processing or DFM failures.
- [`understand-fabrication`](https://www.skills.sh/fabworkshq/fabworks-plugin/understand-fabrication): Collects manufacturing requirements from STEP files and part descriptions, and explains DFM results and material options without guessing unsupported details.

Read the [Fabworks MCP documentation](https://www.fabworks.com/resources/developers/mcp) for setup instructions, available tools, and example quote requests.
