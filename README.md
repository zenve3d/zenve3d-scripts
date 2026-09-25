# zenve3d-scripts

Community-shared `.zcmd` scripts for [Zenve3D](https://zenve3d.com) — parametric parts, fixtures and reference bodies you can import into your own projects.

A `.zcmd` file is a **parametric CAD recipe**, not a mesh: one command per line, replayed by the Zenve engine into sketches, constraints, dimensions and solid features. Every number can be an expression over named `param`s, so an imported part comes with sliders and stays editable.

## What's here

| Folder | Contents |
|---|---|
| `parts/` | Reusable parts and reference bodies — motors, boards, hardware you design *around* — plus printable fixtures like insert bosses |

### Parts

| Script | Description | Key params |
|---|---|---|
| [`parts/nema17.zcmd`](parts/nema17.zcmd) | NEMA 17 stepper motor: chamfered housing, pilot boss, 4× M3 holes on the 31 mm square, D-flat shaft. Housing and shaft are separate bodies so brackets can cut against either. | `bodyL`, `shaftD`, `shaftL`, `holeSpan` |
| [`parts/gt2_pulley_20t.zcmd`](parts/gt2_pulley_20t.zcmd) | GT2 timing pulley, 20T, 5 mm bore: 16 mm flanges, 7.5 mm tooth ring for 6 mm belt, 12 mm hub with two M3 set screws at 90°. `teeth` drives both the outer diameter and the groove count, so 16T or 36T is one slider. Fits the NEMA 17 shaft. | `teeth`, `boreD`, `beltW`, `flangeD`, `hubH` |
| [`parts/m3_heat_insert.zcmd`](parts/m3_heat_insert.zcmd) | M3 heat-set insert boss: 8 mm printable boss with the 4.0 × 6.5 mm pocket for a standard M3 × 5.7 brass insert, a lead-in chamfer at the mouth and a screw-tip clearance pocket below. Join it into a wall or floor. | `insertD`, `pocketH`, `bossD`, `bossH`, `lead` |
| [`parts/arduino_uno.zcmd`](parts/arduino_uno.zcmd) | Arduino Uno R3: official PCB outline and mounting holes, USB-B and barrel jack overhangs, headers with pin holes, main ICs, caps, reset button and LEDs. Each component is its own body with its own colour. | `pcb`, `usb_over`, `jack_over`, `hdr_h` |

## Using a script

1. Download the `.zcmd` file (or clone this repo).
2. In Zenve3D:
   - **Mac:** File ▸ **New from Script…** and pick the file.
   - **iPad:** on the Projects screen, tap **Import** and pick the file.
3. The script runs into a new project and the builder opens on it. Adjust the `param` values in the parameters panel to fit your build.

To drop a part into an *existing* project, paste the script into the **Scripts** panel and run it there; it lands as a new part beside what you already have.

## Contributing a script

Pull requests are welcome, one script per PR. Build it in Zenve3D first, keep it parametric, and include a screenshot of the part and a note on where the dimensions came from. The full guidelines and the PR checklist are in [CONTRIBUTING.md](CONTRIBUTING.md).

## Reporting a problem

If a script fails to run or a dimension is wrong, [open an issue](https://github.com/zenve3d/zenve3d-scripts/issues) with the script name, the Zenve3D version, and the engine's error line.

## License

Everything in this repository is released under the [MIT License](LICENSE). By contributing a script, you agree to license it under the same terms.
