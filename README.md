# Fabworks plugin

Connect an AI coding agent to [Fabworks](https://www.fabworks.com) for sheet-metal and tube manufacturing quotes.

## Install

Install the plugin, MCP configuration, and skills:

```bash
npx plugins add FabworksHQ/fabworks-plugin
```

Install an individual Agent Skill:

```bash
npx skills add FabworksHQ/fabworks-plugin --skill quote-with-fabworks
npx skills add FabworksHQ/fabworks-plugin --skill understand-fabrication
```

The MCP connection uses browser-based OAuth. The server is available at `https://api.fabworks.com/mcp`.

## Included skills

- `quote-with-fabworks`: Create quotes without putting STEP file bytes into agent context, resolve exact catalog configurations, and handle processing or DFM failures.
- `understand-fabrication`: Interpret sheet and tube manufacturing intent and explain quote results without guessing unsupported details.

MCP documentation is available at [fabworks.com/resources/developers/mcp](https://www.fabworks.com/resources/developers/mcp).
