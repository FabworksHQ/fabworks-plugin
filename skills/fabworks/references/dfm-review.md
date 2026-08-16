# Reviewing DFM results and quote failures

Fabworks analyzes every uploaded STEP file and returns design-for-manufacturing findings with the quote. Through the MCP server, `get_quote` with `view: "full"` returns the available parser findings as per-part `dfm_issues`, each with a `code`, `severity`, and `message`. This list is not exhaustive: the quote page at the `checkout_url` can compute and show additional interactive checks for configuration, tooling, bends, and hole operations. Use that page for the complete DFM review.

## Severities

- `error`: the part cannot be manufactured as designed or configured. Resolve it before ordering.
- `warning`: manufacturable, but a flagged risk. Example: missing bend reliefs, or a cutting angle over 45 degrees that may need minor geometry modification.
- `info`: advisory only, such as non-perpendicular cuts on tube edges or a detected flat hem.

Always separate blocking errors from warnings and info when reporting to the user, and quote the returned message rather than paraphrasing the defect.

## Processing failures

When a quote's status is `failed`, one or more files could not be processed, and the result lists each failed file with a `stage`, `code`, and `message`. Documented causes include:

- Unreadable or corrupted STEP file, or an unsupported format
- No solid bodies in the file, or non-solid components in an assembly
- Geometry not recognizable as a laser-cuttable sheet metal or tube part
- Unfoldable sheet designs: overlapping flat pattern or an impossible bend configuration
- Unusually large geometric tolerances suggesting gaps or broken geometry

Report the failure per file. Ask for a corrected export or a design decision; do not retry the same bytes, and do not hide one failed file inside an otherwise successful quote.

## What to review

Returned findings and checkout-page checks map to the documented design rules. Use the matching reference to explain and fix them:

- Flange below minimum length, critical features inside the distortion zone, bend angle past the tooling maximum, reverse bends outside the punch clearance envelope: see [bending.md](bending.md).
- Holes or features below the minimum size for the material and thickness, tube holes too close to edges or crossing the corner radius: see [laser-cutting.md](laser-cutting.md).
- Unsupported tap, countersink angle, counterbore dimensions, or hardware size: see [hole-operations.md](hole-operations.md).
- Material or finish not in the stocked catalog: see [materials-and-finishes.md](materials-and-finishes.md).

## Proposing fixes

Suggest only documented remedies: lengthen a flange, move a feature out of the distortion zone, thicken a tube wall or switch a tap to a press-in nut or insert, pick a supported counterbore size, split a part that fails reverse-bend clearance and join with hardware or welding, or choose a stocked material. When a fix changes design intent, present the option and let the user decide.
