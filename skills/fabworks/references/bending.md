# Bending design rules

The press brake bends sheet up to 0.250" thick and up to 96" long. The quoting engine flags parts outside these rules before ordering.

## Bendable range

- Thickness: 0.030" to 0.250".
- Documented bending materials: Aluminum 5052-H32, Steel 1008, Steel A36, Stainless Steel 304-2B, Galvanized Steel G90. Aluminum 6061-T6 and 7075-T6 sheet are stocked for cutting but are not in the documented bending material list; confirm bendability through a quote before designing bends in them.
- Maximum bend length: up to 96", depending on material and thickness.
- Maximum bend angle and bend radius are set by the tooling for each material and thickness. The per-stock values are in the live bending table at fabworks.com/resources/guidelines/bending; do not quote them from memory.

## Flange length

- Minimum flange length is the straight material between a bend and the sheet edge, measured to the apex of the bend, not the flat face.
- The minimum depends on the selected V-die and the bend angle. Material and thickness can change which V-die is used, but for the same tooling and angle, thickness does not change the minimum.
- Recommend flanges at least 1/16" above the calculated minimum when the design allows. Flanges below minimum can slip into the V-die or buckle.

## Distortion zone

- The area near a bend where material stretches, approximately 75% of the minimum flange length measured from the bend apex.
- Holes can go oval, slots can skew, and edges can crack inside this zone. Keep critical holes, slots, and edges outside it. Non-critical features may extend into it with reduced accuracy.
- The minimum flange length itself depends on the live tooling table, so the exact zone cannot be computed offline. When a feature sits close to a bend, say it is at risk and let the quote's DFM check give the authoritative answer.

## Reverse bends

A reverse bend is any bend where the punch must enter a channel formed by an earlier bend: Z-bends, joggles, U-channels, return flanges, and boxes. Punch clearance sets the limit, and tooling clearance can block a part even when the bend angle alone is allowed. If a reverse bend does not fit the clearance envelope, the documented alternatives are changing the design or splitting the part and joining it with welding or hardware.

## Tolerances

- Single bends: +/-0.015" length and +/-1 degree angle.
- Features separated by multiple bends: an additional +/-0.015" per separating bend.
- Die marks are visible on all bends.

## K-factor

CAD defaults of 0.4 to 0.45 work with the standard tooling and materials. Only override for tight stack-up tolerances, and get the exact value for the specific stock from support@fabworks.com.

## What cannot be bent

- Single bends longer than 96"
- Bends past the maximum angle listed for that material and thickness
- Reverse bends that exceed the punch clearance envelope
- Materials not in the standard inventory
