# Anycubic Kobra X target

This fork is being developed primarily for **Anycubic Kobra X** FFF/FDM use.

## Verified hardware envelope

The development assumptions below follow Anycubic's published Kobra X specifications and user manual:

- Printing technology: FDM / FFF
- Build volume: **260 x 260 x 260 mm**
- Standard nozzle: **0.4 mm**
- Nozzle maximum temperature: **300 C**
- Heated bed maximum temperature: **100 C**
- Extrusion: direct drive
- Firmware family: Kobra OS
- Supported materials include PLA, PETG, TPU and other materials documented by Anycubic
- Anycubic documentation lists PrusaSlicer as a supported slicer

## Reinforced Cut design constraints for Kobra X

The Reinforced Cut tool is geometry-first. It must not depend on a Prusa printer profile or Prusa-specific G-code.

For large hollow sculpture / bust workflows:

1. Each resulting printed part must fit inside a 260 x 260 x 260 mm build volume.
2. Existing PrusaSlicer planar Cut behavior stays available.
3. Existing multiple connector placement stays available.
4. Reinforcement is created toward the hollow interior of the model only.
5. The exterior cosmetic shell must not be displaced or expanded by reinforcement generation.
6. The preferred inner opening is a simple safe oval / ellipse, not a naive offset copy of a highly concave cut contour.
7. Reinforcement must remain manifold after boolean operations.
8. If safe complete reinforcement cannot be generated, the operation must fail explicitly instead of silently creating a partial ring.
9. Connector booleans are applied after the reinforcement body is generated so connector placement is independent from reinforcement shape.

## Print-profile policy

Do **not** invent Kobra X start/end G-code in this fork.

The geometry feature can be tested independently of machine G-code. A Kobra X machine preset should be based on an official Anycubic PrusaSlicer profile or a profile exported from the user's Anycubic software, then checked before being bundled.

This prevents the geometry work from accidentally changing homing, purge, leveling, multicolor, or Kobra OS specific commands.

## Initial validation model

The first production validation target is a large hollow bust / sculpture cut into several pieces for FDM printing. The exterior surface is the critical cosmetic surface; internal reinforcement exists to keep sections aligned and strong enough for assembly / filling.
