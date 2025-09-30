# freecad-quickmacro
FreeCAD macro that fills a base, either a generated cylinder or an imported STEP, with many randomly placed small cylinders using a spatial grid, overlap checks and strict containment via boolean and surface sampling. Includes an optional parameter GUI and exports STL and STEP.

Fill Cylinder Optimized (FreeCAD Macro)
A FreeCAD macro to densely populate a base volume — either a generated cylinder or an imported STEP — with randomly oriented small cylinders. The macro uses a spatial grid for efficient neighbor queries, geometric overlap checks, strict containment tests (boolean intersection plus surface sampling), and optional GUI parameter editing. Exports results to STL and STEP.Features

Use a generated base cylinder or import a STEP as the containment volume.
Randomized sampling with reproducible seed.
Spatial grid acceleration for neighbor searching.
Avoids overlaps with tunable allowed penetration.
Strict containment checks: boolean volume intersection and dense surface/endcap sampling.
Optional Qt GUI to edit parameters before run.
Export small cylinder pack or the base as STL and STEP.
Configurable attempts limit, spacing, sizes, and export options.

Requirements

FreeCAD with Python support.
Part and Mesh modules (standard in FreeCAD).
PySide or PySide2 for the GUI (optional; script runs without GUI).
Access to filesystem for export.

Installation

Copy the macro file fill_cylinders_optimized_with_gui.FCMacro into your FreeCAD macros folder:
FreeCAD → Macro → Macros... → Create or place file in the shown directory.


Alternatively, place it in a project folder and run from FreeCAD Python console.

Usage

Launch the macro from FreeCAD (Macro → Macros → select and Execute).
If GUI is available and use_gui is true, a dialog appears to edit parameters. Edit values and click OK.
The macro will:
Create or reuse a document named by doc_name.
Import a STEP if use_step_as_base and step_path are provided; otherwise generate a cylinder using base_radius, base_height and base_center.
Sample points inside the base and attempt to place oriented small cylinders (small_radius, small_length) while enforcing min_spacing, avoid_overlap, and max_overlap rules.
Perform strict containment and a final boolean volume check.
Export either separate smalls (STL + STEP) or the base object as STL + STEP to export_dir using export_prefix.



Key Parameters (defaults in code)

doc_name: Document name used/created.
seed: Random seed for reproducibility.
use_step_as_base, step_path: Use an imported STEP file as base when set.
base_radius, base_height, base_center: Generated cylinder parameters.
n_target: Target number of small cylinders (0 = fill until attempts exhausted).
small_radius, small_length: Dimensions of the small cylinders.
min_spacing: Minimum center-to-center spacing to accelerate rejection.
avoid_overlap: Toggle geometric overlap avoidance.
max_overlap: Allowed penetration before rejecting placement.
max_attempts: Max sampling attempts.
vol_tol, point_tol: Tolerances used in containment and boolean tests.
export_dir, export_prefix, export_separate, stl_binary: Export settings.
use_gui: Show parameter dialog if Qt is available.

Adjust these directly in the macro or via the GUI.Output

Console logs: progress, counts of attempts, accepted placements and rejection reasons.
Exports:
If export_separate is true: files {prefix}_smalls.stl and {prefix}_smalls.step containing the placed small cylinders.
Otherwise: {prefix}_result.stl and {prefix}_result.step containing the base object (unchopped).


Temporary objects are cleaned up after export.

Notes and Recommendations

For complex or highly concave shapes, increase sampling attempts and containment sampling density (n_axial, n_azimuth, n_endcap_radial inside the containment function) for robustness at higher cost.
Turning off GUI updates improves performance during heavy operations.
If using STEP as base, ensure the STEP contains at least one solid; the script picks the last suitable object after import.


Troubleshooting

If Qt is not available the macro runs with defaults and no dialog.
If STEP import fails, the macro falls back to the generated cylinder.
If exports fail, check write permissions for export_dir.

Contact / Support
marczis.a.1@gmail.com

License

MIT License
Copyright (c) 2025 MarczisA
Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
