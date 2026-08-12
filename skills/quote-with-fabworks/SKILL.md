---
name: quote-with-fabworks
description: Create and manage Fabworks online laser cutting quotes through the Fabworks MCP server. Use when a user asks an agent to quote STEP files or laser-cut sheet metal or tube parts, find Fabworks materials or finishes, review quote pricing or DFM results, update quote parts, list recent quotes, or check a Fabworks order.
---

# Quote with Fabworks

Use the Fabworks MCP tools at `https://api.fabworks.com/mcp`.

## Create a quote

1. Confirm the STEP files, quantities, part names, material, finish, and optional quote name. Ask only for values that affect the requested quote.
2. Call `find_materials` with structured filters. Use exact catalog IDs in later calls.
3. If the result contains only suggestions, show the relevant choices and ask the user. Never silently substitute a nearby thickness, grade, profile, or finish.
4. Call `create_upload` once for each STEP file.
5. Upload each file directly to its signed URL with the returned HTTP method and headers. Do not read the file as base64 or put its bytes in the conversation.
6. Call `create_quote` once with the upload IDs and resolved catalog IDs. Generate an `idempotency_key` locally so a transport retry cannot create a duplicate quote.
7. Use the returned result. If its status is still processing, call `get_quote`; the default wait is suitable for an agent. Do not create the quote again.
8. Report the quote number, status, total price, part configuration, important DFM results, and checkout URL. State clearly when pricing is not ready.

## Update and inspect

- Use `list_quotes` to find a quote by its name or number.
- Use `get_quote` with `view: "summary"` for routine polling. Request `view: "full"` only when part-level detail is needed.
- Use `update_quote_parts` to rename parts or change quantities, materials, and finishes. Generate one idempotency key for the requested update.
- Use `check_order_status` only after the user supplies or selects an order.
- Do not imply that a quote was ordered or paid. The MCP server does not submit checkout.

## Handle results safely

- Treat `exact` matches and `suggestions` differently. A suggestion always needs user confirmation.
- Treat `box`, `square`, and `rectangular` as equivalent search terms for rectangular tube, but still match width, height, wall thickness, material type, and grade.
- Use decimal thickness when possible. Gauge names can differ by material.
- If a file fails, report its stage, code, and message. Do not hide a failed part inside a successful multi-part result.
- Preserve upload IDs returned with `needs_input`; resolve the missing choice and retry with those IDs instead of uploading the file again.
- Never expose API keys, OAuth tokens, signed upload URLs, or raw CAD data in the answer.
