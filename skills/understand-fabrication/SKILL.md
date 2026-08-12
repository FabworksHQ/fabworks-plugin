---
name: understand-fabrication
description: Interpret STEP files and manufacturing requirements for Fabworks laser cutting. Use when the user needs to tell sheet from tube parts, choose a material, thickness, tube profile, or finish, understand DFM results, or turn a part description into a precise Fabworks quote request.
---

# Understand fabrication

Use this skill to collect and explain manufacturing intent. Do not calculate a binding Fabworks price or invent a process capability.

## Describe each part

Collect only the facts needed for the task:

- Process family: flat sheet, bent sheet, or tube.
- Material type and grade.
- Sheet thickness, or tube profile dimensions and wall thickness.
- Quantity and part name.
- Finish.
- Any requirement that is not fully represented by the STEP geometry.

Prefer decimal inches or millimeters over gauge names. If the user gives a gauge, keep the material type with it because gauge thickness varies by material.

## Interpret geometry

- A flat or bent sheet part has a substantially constant material thickness.
- A tube part needs its profile family and dimensions. Record width and height for rectangular tube, diameter for round tube, and wall thickness for both.
- `Box`, `square`, and `rectangular` can describe the same rectangular tube family. A square tube has equal width and height.
- Do not infer a catalog material from color, filename, or geometry.
- Do not assume that a modeled hole specifies tapping, countersinking, counterboring, or hardware. Ask when the requested operation is not explicit.

## Review a quote

- Treat Fabworks catalog IDs, computed price, and DFM output as authoritative for the quote.
- Explain the exact material, finish, quantity, and process returned for each part.
- Separate blocking DFM failures from warnings and informational results.
- If a catalog search returns alternatives, explain the difference and let the user choose. Never substitute a nearby gauge, alloy, tube size, or finish without approval.
- If CAD processing fails, report the file-specific failure. Ask for a corrected STEP file or a clear design decision instead of repeatedly retrying the same input.

Read [fabrication-reference.md](references/fabrication-reference.md) when the user needs a concise comparison of part families, dimensions, or finishes.
