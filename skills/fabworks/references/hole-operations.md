# Hole operations and hardware

Tapping, countersinking, counterboring, and hardware installation are add-on operations on laser-cut parts. Supported sizes for taps and hardware are live catalog data on the guidelines pages at fabworks.com/resources/guidelines (tapping, countersinking, hardware); only the counterbore table below is documented in full.

## Tapping

- Creates internal threads in pre-cut holes for screws and bolts.
- Supported tap sizes are listed only in the live table at fabworks.com/resources/guidelines/tapping; do not quote sizes from memory, and do not infer that a tap size exists because the same screw size appears in the counterbore table below.
- On tube: tapped holes need at least three full threads of engagement, and walls thinner than 0.083" should use a press-in nut or threaded insert instead.
- No minimum sheet thickness per tap size is documented. For thin sheet where tapped threads would be weak, clinched hardware is the documented alternative; otherwise rely on the quote's DFM feedback.
- How to pre-size a hole that will be tapped is not documented. Configure the tap during quoting and follow the quote's feedback.
- Whether tapped holes are masked during powder coating is not documented. When a part is both tapped and powder coated, tell the user to arrange masking with support@fabworks.com before ordering.

## Countersinking

- Creates a tapered seat so flat-head fasteners sit flush or below the surface.
- Any countersink diameter is accepted when the angle is 82, 90, 100, or 120 degrees. Model countersinks directly in the STEP file; the same four angles are what the DFM checks accept.
- A countersink can also be added to an existing hole through the hole operations selector, from the documented countersink list.
- Tolerance is -0.000"/+0.015", which seats bolts sub-flush.
- Large countersinks in thin material enlarge the through-hole diameter; account for this in fitment.
- Powder coating adds roughly 0.004" of thickness; account for it when a sub-flush fit is critical.

## Counterboring

- Creates a flat-bottom recess with a cylindrical wall for socket head cap screws and other cylindrical-head machine screws.
- Counterbores must be modeled directly in the STEP file. They cannot be added from the hole operations selector.
- Any depth is accepted when the body and pilot diameters match a supported size. Depth tolerance is +0.015"/-0.000".

Supported counterbore dimensions:

| Screw | Body dia. | Pilot dia. |
| --- | --- | --- |
| #4 | 0.206" | 0.128" |
| #6 | 0.244" | 0.154" |
| #8 | 0.288" | 0.180" |
| #10 | 0.330" | 0.206" |
| 1/4" | 0.398" | 0.266" |
| 5/16" | 0.491" | 0.328" |
| M3 | 6.0 mm | 3.5 mm |
| M4 | 7.5 mm | 4.5 mm |
| M5 | 9.0 mm | 5.5 mm |
| M6 | 10.5 mm | 6.5 mm |
| M8 | 13.5 mm | 8.5 mm |

## Hardware

- Self-clinching fasteners installed into pre-cut holes: PEM nuts, flush nuts, studs, standoffs, blind standoffs, and rivnuts.
- Use hardware where tapped threads in thin sheet would be too weak; clinched hardware provides load-bearing threads in thin material.
- Model hardware holes at the hardware's callout size. Fabworks resizes them automatically to the correct press-fit dimension.
- Supported part numbers and size-versus-thickness limits are in the live tables at fabworks.com/resources/guidelines/hardware; do not quote them from memory.
