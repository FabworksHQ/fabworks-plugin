# Laser cutting design rules

## Both sheet and tube

- Do not compensate for kerf in the CAD file. Model features at their intended final size.
- Standard cutting tolerance is +/-0.005" across the whole part: hole sizes, outer dimensions, and hole-to-hole. Most parts come out around +/-0.002".
- Tolerance can open up on very long thin parts that deform while cutting, thick parts with many cutouts that build heat, and features located relative to tube edges (typically +/-0.010").
- Cut edges taper about 0.001" for every 0.1" of material thickness, so edges are not perfectly perpendicular.
- Expect a clean edge with minimal burrs and heat-affected zone. Deburring is an optional finish.
- Engraving is not offered.

## Sheet

Cut on a 4kW TRUMPF TruLaser 1030 fiber laser.

- Maximum part size 96" x 47", minimum 0.25" x 0.25". Parts that will be bent are limited to 80 lbs.
- Minimum hole and feature size depends on material and thickness. The per-thickness limit is listed in the live material tables at fabworks.com/resources/materials; do not quote a number from memory.
- Model holes intended for hardware at the hardware's callout size. Fabworks resizes them automatically to the correct press-fit dimension.

## Tube

Cut on a 5-axis TRUMPF TruLaser Tube 5000 fiber laser, which cuts holes, tabs, slots, copes, miters, and bevels in a single setup.

- Round, square, and rectangular tube in steel and aluminum.
- Maximum finished part length 96". Length tolerance is +/-0.020", which accounts for cutoff from raw stock and end squareness.
- Do not model the corner edge radius on square or rectangular tube. Sharp CAD corners are correct; the physical radius varies with each stock batch.
- Minimum hole diameter is 0.020" regardless of wall thickness or material.
- Keep holes at least one wall thickness away from any tube edge or end cut.
- On square tube, place holes on the flat face rather than across the corner radius. Holes crossing the corner distort because the surface is curved through the kerf path.
- Tapped holes need at least three full threads of engagement. On walls thinner than 0.083", use a press-in nut or threaded insert instead of tapping.

Supported end conditions and joining features, all cut in one operation:

- Square cuts perpendicular to the tube axis
- Miters up to +/-45 degrees, including compound miters rotated and tilted in one cut
- Copes (fish mouths) for tube-to-tube intersections
- Bevels for weld preparation
- Tab-and-slot features for self-locating assemblies
