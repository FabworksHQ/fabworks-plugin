---
name: fabworks
description: Quote and manage Fabworks online laser cutting work, or answer Fabworks fabrication questions. Use when the user asks to quote or price STEP files; order laser-cut flat sheet, bent sheet, or tube parts; find materials, tube profiles, thicknesses, or finishes; review pricing, DFM results, or quote failures; update quote parts; check an order; decide whether Fabworks can make a part; compare fabrication options; or understand documented laser cutting, bending, tapping, countersinking, counterboring, hardware, powder coating, material, and finish rules. Works with or without a live Fabworks MCP connection.
---

# Fabworks

Use this skill as the single entry point for Fabworks. Use the MCP tools when the task changes or reads a live quote, catalog, or order. Use the bundled references when the task needs fabrication knowledge.

Do not invent process capabilities, tolerances, lead times, pricing rules, or stocked materials. If a fact is not documented, say so and direct the user to support@fabworks.com.

## Create a quote

Use the Fabworks MCP server at `https://api.fabworks.com/mcp`. Use `create_quote`, not the deprecated `quote_parts` alias.

1. Confirm the STEP files, quantities, part names, material, finish, and optional quote name. Ask only for missing values that affect the quote. A missing finish means No Deburring.
2. Call `find_materials` with structured filters. Use exact catalog IDs in later calls.
3. If the result contains only suggestions, show the relevant choices and ask the user. Never silently substitute a nearby thickness, grade, profile, or finish.
4. Call `create_upload` once for each `.step` or `.stp` file.
5. Upload each file directly to its signed URL with the returned HTTP method and headers. Do this before the URL expires. Do not read the file as base64 or put its bytes in the conversation.
6. Call `create_quote` once with the upload IDs and exact catalog IDs. One call accepts 1 to 25 STEP inputs. Each input can have its own material, finish, name, and quantity. Generate one local `idempotency_key` so a transport retry cannot create a duplicate quote.
7. If the quote is still processing, call `get_quote`. Do not create the quote again.
8. Report the quote number, status, total price, part configuration, every DFM error and warning, and the checkout URL. State clearly when pricing is not ready. When `dfm.checkout_blocked` is true, say the quote cannot be ordered until the errors are fixed. Never say a part has no manufacturability issues unless `dfm.errors` and `dfm.warnings` are both 0, and mention that bent parts get one more bend-sequence check on the checkout page. For a bent part with issues, give its `bending_url` so the user can watch the bend sequence.

Read [tool-results.md](references/tool-results.md) before handling `needs_input`, suggestions, failures, multipart STEP files, polling, updates, or any result field that is not clear.

## Manage quotes and orders

- Use `list_quotes` to find a quote by name or number.
- Use `get_quote` for polling and review. Every ready result includes DFM results. `view: "full"` adds part geometry (type, bend count, flat size).
- Use `update_quote_parts` to rename parts or change quantities, materials, and finishes. Generate one idempotency key for the requested update. Report the refreshed DFM results, since a material or thickness change can add or clear errors.
- Use `check_order_status` only after the user supplies or selects an order.
- Do not imply that a quote was ordered or paid. The MCP server does not submit checkout or payment.

## Handle live results safely

- Treat exact matches and suggestions differently. A suggestion always needs user confirmation.
- Treat `box`, `square`, and `rectangular` as equivalent search terms for rectangular tube. Still match width, height, wall thickness, material type, and grade.
- Use decimal thickness when possible. Gauge names can differ by material.
- If a file fails, report its stage, code, and message. Do not hide a failed part inside a successful multipart result.
- Preserve upload IDs returned with `needs_input`. Resolve the missing choice and retry with those IDs instead of uploading the file again.
- Never expose API keys, OAuth tokens, signed upload URLs, or raw CAD data.

## Understand a part

Classify the geometry before giving fabrication advice:

1. Treat substantially constant thickness on one plane as flat sheet.
2. Treat substantially constant thickness folded along bend lines as bent sheet.
3. Treat a hollow profile with constant wall thickness as tube. Record outside diameter and wall for round tube. Record width, height, and wall for square or rectangular tube.
4. Treat bulk geometry with a varying cross-section as likely unsupported unless the variation is a documented hole operation.

Check common mistakes: swapped width and height, outside diameter confused with inside diameter, nominal wall confused with measured wall, and gauge stated without its material.

Do not infer material from color, filename, or geometry. Do not assume that a modeled hole requires tapping, countersinking, counterboring, or hardware. Ask when the operation is not explicit.

## Collect fabrication requirements

Gather only the facts that the task needs:

- Process family: flat sheet, bent sheet, or tube.
- Material type and grade.
- Sheet thickness, or tube profile dimensions and wall thickness.
- Quantity and part name.
- Finish. A missing finish means No Deburring.
- Any requested hole operation or requirement that the STEP geometry does not represent.

Use live `find_materials` results for exact stocked thicknesses, tube profiles, and finishes. It does not search tap or hardware sizes. Use the documented guideline references for those operations.

## Load the needed reference

Read only the references that apply to the task.

| Need | Read |
| --- | --- |
| MCP fields, statuses, suggestions, failures, and polling | [tool-results.md](references/tool-results.md) |
| Fabworks services, boundaries, file rules, size limits, and lead times | [services.md](references/services.md) |
| Laser cutting tolerances, kerf, taper, sheet limits, tube limits, and end cuts | [laser-cutting.md](references/laser-cutting.md) |
| Bend limits, flanges, distortion zones, reverse bends, and tolerances | [bending.md](references/bending.md) |
| Tapping, countersinking, counterboring, and hardware | [hole-operations.md](references/hole-operations.md) |
| Material families, grades, finishes, and powder coating | [materials-and-finishes.md](references/materials-and-finishes.md) |
| DFM severity, processing failures, and documented fixes | [dfm-review.md](references/dfm-review.md) |

Treat live catalog IDs, computed prices, and MCP DFM results as authoritative for that quote. They use the same checks as checkout, except the bend-sequence simulation, which runs only on the checkout page. The checkout URL opens in the Fabworks account that owns the quote, so tell the user to sign in to that account first.
