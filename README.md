# zenve3d-scripts

Community-shared `.zcmd` scripts for [Zenve3D](https://zenve3d.com) — parametric parts, fixtures and reference bodies you can import into your own projects.

A `.zcmd` file is a **parametric CAD recipe**, not a mesh: one command per line, replayed by the Zenve engine into sketches, constraints, dimensions and solid features. Every number can be an expression over named `param`s, so an imported part comes with sliders and stays editable.

## What's here

| Folder | Contents |
|---|---|
| `parts/` | Reusable parts and reference bodies — motors, boards, hardware you design *around* |

### Parts

| Script | Description | Key params |
|---|---|---|
| [`parts/nema17.zcmd`](parts/nema17.zcmd) | NEMA 17 stepper motor: chamfered housing, pilot boss, 4× M3 holes on the 31 mm square, D-flat shaft. Housing and shaft are separate bodies so brackets can cut against either. | `bodyL`, `shaftD`, `shaftL`, `holeSpan` |
| [`parts/arduino_uno.zcmd`](parts/arduino_uno.zcmd) | Arduino Uno R3: official PCB outline and mounting holes, USB-B and barrel jack overhangs, headers with pin holes, main ICs, caps, reset button and LEDs. Each component is its own body with its own colour. | `pcb`, `usb_over`, `jack_over`, `hdr_h` |

## Using a script

1. Download the `.zcmd` file (or clone this repo).
2. In Zenve3D:
   - **Mac:** File ▸ **New from Script…** and pick the file.
   - **iPad:** on the Projects screen, tap **Import** and pick the file.
3. The script runs into a new project and the builder opens on it. Adjust the `param` values in the parameters panel to fit your build.

To drop a part into an *existing* project, paste the script into the **Scripts** panel and run it there; it lands as a new part beside what you already have.

## Contributing a script

Pull requests are welcome. Please make sure your script:

- **Starts with `zcmd 1`** and runs cleanly end to end in the current Zenve3D release.
- **Is parametric.** Open with `param` lines for anything someone would want to change (overall size, hole diameters, clearances) and reference them in expressions instead of hard-coding numbers.
- **Has a header comment** saying what the part is, where its origin sits, which axis the important feature points along, and which dimensions are official versus typical.
- **Avoids guessed indices.** Prefer datum planes (`plane on XY offset …`) over `face(BODY, I)` where a position is expressible from an origin plane. Where indices are unavoidable, guard them with `!assert` lines so a breaking change fails loudly.
- **Names its output.** Use `rename body` / `rename feature` so the tree reads well, and set `material` colours where they help recognition.
- **Ends with asserts** on `bodies`, `bbox` and `stl closed` so reviewers and future engine versions can verify it.
- Uses **millimetres** and a **lowercase snake_case filename** describing the part (`nema17.zcmd`, `arduino_uno.zcmd`).

Open a PR against `main` with the script and one line added to the table above. Include a screenshot in the PR description if you can.

For the full command reference and authoring workflow, see the [`.zcmd` authoring guide](https://github.com/zenve3d/zenve3d/blob/main/docs/zcmd-authoring.md) in the main Zenve3D repo.

## Reporting a problem

If a script fails to run or a dimension is wrong, [open an issue](https://github.com/zenve3d/zenve3d-scripts/issues) with the script name, the Zenve3D version, and the engine's error line.

## License

Everything in this repository is released under the [MIT License](LICENSE). By contributing a script, you agree to license it under the same terms.
