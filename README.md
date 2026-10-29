# PicoEnclosure

A 3D-printable back shell for a Kern device built from an **ESP32-P4-Pico** board and a
**5" DSI touch display** (050-DSI-TOUCH-A), modelled in [SolidCraft](https://github.com/bherbruck/solidcraft).

The display keeps its own case; the shell closes its back. It screws to the display's four
corner standoffs and holds the board, which sits in a keel below the main floor. The camera
looks out through a window in the back, and the USB-C port and the microSD slot are reached
through one opening in the side wall.

Work in progress: the back shell is modelled; print orientation and a front lip or bezel are
still open.

## Files

| File | What it is |
|---|---|
| `pico_enclosure.sc` | Assembly: display, board, camera and back shell in place |
| `back_shell.sc` | The printed part, fully parametric |
| `display_5in_dsi.sc` | Simplified display model (panel, back plate, standoffs) |
| `esp32_p4_pico.sc` | Board model, imported from the vendor's STEP file |
| `exports/` | `BackShell.stl` and `BackShell.3mf` for printing, `display_5in_dsi.step` |

The assembly links its parts by relative path, so keep the `.sc` files together.

## Opening the designs

Use SolidCraft 0.25.1 or newer; older releases cannot read this design format. Open
`pico_enclosure.sc` for the whole device, or `back_shell.sc` to edit the shell. After saving a
part, run **Update Links** in the assembly to bring the change in.

## Back shell

- Outside 129 × 72.8 mm with R4 corners, matching the display; 9.6 mm deep, 22.2 mm at the keel.
- Walls and floor 2 mm.
- Display mounting: four M2.5 screws through counterbored holes into the display's standoffs.
- Board mounting: four tapered posts with Ø1.3 mm pilot holes for M1.6 screws.
- 45° ramp at the end of the keel and 45° gussets on the corner mount blocks, to print without
  supports.

The shell is driven by named user parameters (Parameters table, each with a comment), among them
`shell_w`, `shell_h`, `wall`, `floor_t`, `cavity_depth`, `pocket_depth`, `mount_x`, `mount_y`,
`mount_reach`, `mount_reach_y`, `pcb_depth`, `post_x1`, `post_x2`, `post_y`, `lens_x`, `ramp_r`
and `ramp_x`.

Coordinate frame for every part: origin at the centre of the display's back face (the mounting
plane), +Z toward the viewer, USB-C end at +X.

## Known issue

In SolidCraft 0.25.1, editing a feature that sits in a timeline folder through its dialog can
leave a stale entry in that folder. The design saves, but then fails to open with
`damaged design: invalid feature in a timeline folder`. Before saving, remove the folder and
group its features again, or change values in the Parameters table instead of the dialog.

## License

MIT, see [LICENSE](LICENSE). It covers this project's own files. It does not cover the board
model in `esp32_p4_pico.sc`, which is imported from the vendor's STEP file.
