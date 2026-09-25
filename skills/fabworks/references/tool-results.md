# Fabworks MCP tool results

Field-level behavior of the Fabworks MCP tools. All prices are USD. Errors return a JSON body with `code` and `message`; report both.

## find_materials

- `data` holds matches. With structured filters (`material_type`, `grade`, `thickness`, `tube_subtype`, `width`, `height`, `finish_name`) a result in `data` is an exact match; `match_status` is `matched` or `no_exact_match`.
- `thickness_tolerance` defaults to 0 (exact) and `dimension_tolerance` to 0.01. Widen them only deliberately.
- `suggestions` are labeled alternatives returned when nothing matched exactly. Each carries `match_notes` stating how it differs (for example "thickness is 0.125 in, not 0.12 in"). Never select one without user confirmation.
- Materials return stable `mat_` IDs with `kind` (`sheet` or `tube`), `type`, `grade`, `thickness` (inches), and for tube `subtype`, `width`, `height`. Finishes return `fin_` IDs with `name`, `type`, and color fields.
- `limit` caps total results across all requested categories.

## create_upload

- Accepts only filenames ending `.step` or `.stp`; anything else fails with `unsupported_file_type`.
- Returns `upload_id`, a signed `upload_url`, `method` (PUT), and `headers`. The signed URL expires after `expires_in_seconds` (15 minutes); the upload record itself after `upload_expires_in_seconds`.
- PUT the raw file bytes before creating the quote, or `create_quote` fails with `upload_incomplete`. An expired or foreign upload returns `upload_not_found`; create a new upload.
- Files are capped at 24 MB, and one `create_quote` call shares that 24 MB budget across all its files.

## create_quote

- Takes 1 to 25 STEP inputs. Each input's `source` is an `upload_id`, a public HTTPS `url`, or base64 (avoid base64). Per-input `material_id`/`finish_id` override the top-level defaults. A multipart STEP input can produce multiple quote parts.
- `status: "needs_input"` means a material or finish did not resolve to exactly one catalog entry. The result lists per-part `material_candidates` or `finish_candidates` and returns an `upload` handle for every part, including parts sent by URL or base64. Ask the user to choose, then retry with those upload IDs; never re-send file bytes.
- Reusing the same `idempotency_key` with identical input replays the original quote instead of creating a duplicate; the result then has `idempotent_replayed: true`. Successful non-replayed quotes consume their upload IDs, so a later retry needs fresh uploads.
- `wait_seconds` (0 to 60, default 20) is how long the call may wait for parsing and pricing before returning a processing status.

## get_quote

- `status` is `processing`, `failed`, or `ready`. Default wait is 55 seconds; `wait_seconds: 0` gives an immediate check. Poll with `get_quote`, never by re-creating the quote.
- `failed` results include `files`, each with `filename`, `stage`, `code`, and `message`. Report every failed file individually.
- `ready` results include `parts` (id, name, filename, quantity, `material` as type/grade/thickness, `finish`, `unit_price`, `total_price`, `dfm_issues`) and `pricing.subtotal`. The subtotal excludes shipping and tax. `view: "full"` adds each part's `geometry` (type, subtype, thickness, bends, flat size in inches).
- `dfm` summarizes the checks that checkout runs: `errors`, `warnings`, `checkout_blocked`, and `message`. Each `dfm_issues` entry has `severity` (`error`, `warning`, `info`), `message`, and sometimes `count`. Welded assemblies can add `assembly_dfm_issues`. Report every error and warning. When `checkout_blocked` is true, the user must fix the model or change the configuration before ordering. `not_checked` notes that the bend-sequence simulation runs only on the checkout page.
- Each ready part has `review_url`, which opens the quote scrolled to that part. Bent parts also have `bending_url`, which opens the press brake simulation for that part. Share `bending_url` for a bent part with DFM issues, or when the user wants to see how it bends.
- Every result carries `checkout_url`, the quote page where the user reviews and orders. It opens in the Fabworks account that owns the quote. If the user sees an empty quote, they are signed in to a different account. The MCP server never submits checkout.

## update_quote_parts

- Updates go by `part_id` from a `ready` quote. Only supplied fields change.
- Quantity can only be changed on a standalone part. A part that is still a component of a multipart assembly rejects quantity changes with `invalid_quantity`; report that limit instead of retrying. Invalid part IDs return `part_not_found`, and an unsupported material or finish combination returns `invalid_part_configuration` with an explanatory message. Exception: changing the material by name also resets the finish to the default No Deburring unless a finish is supplied in the same update. Prefer `material_id`, which leaves the finish untouched.
- Ambiguous material or finish input returns `needs_input` with candidates, and nothing is applied. The success result is the refreshed quote, including fresh DFM results.

## check_order_status

- Accepts an order ID or order number. Returns order `status`, per-job statuses, and shipments with tracking numbers and URLs. Unknown orders return `order_not_found`.
