# Contributing a script

Thanks for sharing a part. Every script in this repo arrives as a pull request so it can be tried, reviewed and listed. This page is the whole process.

## 1. Before you start

- Check the `parts/` folder and open PRs so you are not duplicating a part that already exists. If one exists but is wrong or incomplete, improve it in a PR instead of adding a second one.
- Build the script in Zenve3D first and make sure it runs end to end on the current release. The engine's refusals are the review's first pass; a script that does not run will not be merged.

## 2. Script guidelines

**File**

- Lowercase `snake_case` filename that names the part: `nema17.zcmd`, `arduino_uno.zcmd`, `m3_heat_insert.zcmd`.
- Goes in `parts/` (or a new folder if it is clearly a different kind of thing — say so in the PR).
- Millimetres throughout.

**Header**

- First line is `zcmd 1`.
- A comment block at the top saying:
  - what the part is (with the real-world name and variant, e.g. "NEMA 17, 40 mm body");
  - where the origin sits and which axis the important feature points along;
  - which dimensions are official from a datasheet and which are typical, so people know what to double-check against their own hardware;
  - anything the model deliberately leaves out.

**Parametric by default**

- Open with `param` lines for anything someone would want to change: overall size, hole diameters, clearances, heights.
- Reference the params in expressions (`"bodyW / 2"`) instead of repeating literal numbers. A magic number in the middle of a script is a bug waiting for the first person who changes a param.
- Default values should be the real part's dimensions, so importing with no changes gives a correct model.

**Robust geometry**

- Prefer datum planes (`plane on XY offset …`) over `face(BODY, I)` wherever a position is expressible from an origin plane. Face and edge indices come from the engine's decomposition and drift when earlier features change.
- Where an index is unavoidable, guard it with `!assert` lines (`dof`, `regions`, `feature … == ok`) so a wrong index fails loudly instead of landing on the wrong face.
- Keep functionally separate pieces as separate bodies (a motor housing and its shaft, a PCB and its connectors) so a user's bracket or case can cut against one without the other.

**Readable output**

- `rename body` and `rename feature` so the feature tree reads like a parts list, not `Extrude 7`.
- Set `material` colours where they help recognise the part.
- End with asserts on `bodies`, `bbox` and `stl closed`.

**Reference**

The full command reference and the write → run → read loop are in the [`.zcmd` authoring guide](https://github.com/zenve3d/zenve3d/blob/main/docs/zcmd-authoring.md).

## 3. Opening the pull request

One script per PR. The PR template fills in the sections below when you open it; please keep them all.

- **What it is.** One or two sentences: the part, the variant, what it is for (a reference body to design around, a printable part, a fixture).
- **Picture.** A screenshot of the part rendered in Zenve3D, dragged into the PR description. For a reference body, a photo of the real part next to it is a plus.
- **Source of dimensions.** A link to the datasheet or drawing you worked from, or "measured from a physical part" if that is the case.
- **Params worth changing.** Which `param`s a user is most likely to touch and what range makes sense.
- **README row.** Add one line to the parts table in `README.md` for your script.
- **Checklist.** Tick every box in the template. A reviewer will run the script and check the same list.

## 4. Review

A maintainer will import the script on the current Zenve3D release and check the geometry against the header comment and the source you linked. Expect small requests around params, naming and asserts. Once it runs clean and the checklist holds, it is merged and appears in the parts table.

## Reporting a problem with an existing script

[Open an issue](https://github.com/zenve3d/zenve3d-scripts/issues) with the script name, the Zenve3D version, and the engine's error line or a description of the wrong dimension. Fixes are welcome as PRs, same process as above.

## License

By contributing you agree to release your script under the repo's [MIT License](LICENSE).
