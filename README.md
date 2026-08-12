# Fabworks MCP plugin

[![skills.sh](https://skills.sh/b/FabworksHQ/fabworks-plugin)](https://skills.sh/FabworksHQ/fabworks-plugin)

[Fabworks](https://www.fabworks.com) is one of the fastest ways to order laser-cut parts online. Connect an AI coding agent through the remote Model Context Protocol (MCP) server to create online laser cutting quotes for custom sheet metal and tube parts from STEP files, review pricing and DFM results, update quote parts, and check order status.

## What it does

- Finds exact Fabworks materials, tube profiles, thicknesses, and finishes.
- Uploads STEP files through signed URLs so CAD file bytes stay out of the agent context.
- Creates and updates laser cutting quotes for sheet metal and tube parts.
- Returns quote pricing, part configuration, DFM results, and checkout links.
- Uses browser-based OAuth or a Fabworks API key for authentication.

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

- [`quote-with-fabworks`](https://www.skills.sh/fabworkshq/fabworks-plugin/quote-with-fabworks): Create online laser cutting quotes without putting STEP file bytes into agent context, resolve exact catalog configurations, and handle processing or DFM failures.
- [`understand-fabrication`](https://www.skills.sh/fabworkshq/fabworks-plugin/understand-fabrication): Interpret laser-cut sheet metal and tube manufacturing intent and explain quote results without guessing unsupported details.

Read the [Fabworks MCP documentation](https://www.fabworks.com/resources/developers/mcp) for setup instructions, available tools, and example quote requests.
