# mesh-bed-tools

Simple tools for performing mesh profiling of a CNC router bed using LinuxCNC and Python.

A G-Code script for LinuxCNC performs the measurements using a digital touch probe, saving results (controlled location of probe tip at point of contact at each test location) to a text file in space-delimited format.
A Python script reads the data file and can generate various 3D surface plots using scipy, meant to help visualize and diagnose several different possible error contributions. 
* Raw as-probed mesh surface
* Best-fit plane and residual error - helps assess coplanarity of axes with the bed
* Best-fit 'twisted plane' (including X**Y as the only 2nd-order term) and residual error - helps assess twist
* Best-fit quadratic surface and residual error - helps assess cupping/bowing of the bed, or equivalently sag along X or Y axes

## Important Note
It's very important to note that because the machine is measuring its own bed, the measured mesh is influenced by a combination of how flat the bed is, and how straight and well-aligned the axes of motion of the machine are - and from that measurement alone, you can't isolate the two possible sources of error.
A solution is to place a known-flat reference surface (e.g. a granite surface plate) on the bed and probe that - any twist/curvature observed can be attributed to the axes of the machine.

## Mesh bed leveling process
I intend to put together an informational video on a suggested process for using these tools to dial in your CNC router, but in brief:
* Probe a surface plate, isolate and address any curvature by adjusting the machine (e.g. linear guide rail straightness and/or alignment)
* Probe the bed, isolate and address any tilt (coplanarity) error by adjusting the machine (e.g. height of either end of the gantry)
* At this point, any residual error is assumed to be the flatness of the bed itself - adjust it mechanically (e.g. shims) and/or surface it flat using the spindle

This gets the bed flat and coplanar with the XY plane of the machine.  This mesh process doesn't address squareness of X and Y axes, and tram of both the Z axis itself and the spindle - those require different approaches and are left as an exercise for the reader :)

## Future enhancements
These tools could easily be extended to probe laterally, allowing you to probe a precision reference square to assess perpendicularity of X and Y axes to aid in squaring adjustments.