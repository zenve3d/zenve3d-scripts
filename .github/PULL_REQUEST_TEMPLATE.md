## What it is

<!-- The part, the variant, what it is for. One or two sentences. -->

## Picture

<!-- Drag a screenshot of the part rendered in Zenve3D here. -->

## Source of dimensions

<!-- Datasheet / drawing link, or "measured from a physical part". -->

## Params worth changing

<!-- Which params a user is most likely to touch, and a sensible range. -->

## Checklist

- [ ] Runs end to end on the current Zenve3D release with no engine refusals
- [ ] First line is `zcmd 1`
- [ ] Header comment states what it is, origin and axis, official vs typical dimensions
- [ ] Sizes, holes and clearances are `param`s with real-part defaults; no magic numbers in expressions
- [ ] Datum planes preferred over `face(BODY, I)`; remaining indices guarded by `!assert`
- [ ] Functionally separate pieces are separate bodies
- [ ] Bodies and features renamed; materials set where useful
- [ ] Ends with `!assert bodies`, `!assert bbox` and `!assert stl closed`
- [ ] Millimetres; lowercase `snake_case` filename in `parts/`
- [ ] One line added to the parts table in `README.md`
- [ ] I agree to release this under the repo's MIT License
