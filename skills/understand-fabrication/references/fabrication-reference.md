# Fabrication reference

| Part family | Minimum useful description | Common ambiguity |
| --- | --- | --- |
| Flat sheet | Material, grade, thickness, quantity, finish | Gauge without a material type |
| Bent sheet | Material, grade, thickness, quantity, finish | Bend intent not represented in the STEP model |
| Rectangular tube | Material, grade, width, height, wall, quantity, finish | Width and height swapped; nominal wall confused with measured wall |
| Round tube | Material, grade, outside diameter, wall, quantity, finish | Outside diameter confused with inside diameter |

## Finish language

- `No Deburring` means no separate deburring finish.
- `Deburred` removes sharp edges but is not a cosmetic coating.
- Powder coat needs an exact catalog finish. Color names alone can be ambiguous.
- Do not treat raw material appearance as a finish specification.

## Quoting language

- Use exact decimal thicknesses when available.
- Keep tube subtype and all profile dimensions together.
- Use the name in the quote request as the customer-facing part name.
- A quote is an estimate until Fabworks returns a ready result with pricing.
