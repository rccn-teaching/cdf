# Week 04 — Getting it out

> **This page is the reference.** Last Rhino week — Grasshopper starts next.

A model is not finished when it looks right. It is finished when something
**true** can be extracted from it: a drawing at a stated scale, an image, or a
cut file a machine will accept.

---

## 1. `Make2D`

Projects 3D geometry into 2D curves, from the current view or a named one.

- Output lands on **new layers** (`Make2D::visible::lines`…). Wire those into
  your `80_DRAWING` structure immediately, before you lose track of them.
- **Tangent edges** adds the lines where a fillet rolls away. Turning them
  *off* is often what makes a drawing read.
- **Slow on heavy models.** Hide what you do not need first.
- The result is **static**. Change the model, run it again — there is no link.

**`Silhouette`** gives just the outline of an object, live and much faster. For
a massing diagram or a figure-ground it is usually the better tool.

## 2. Annotation

| | |
| --- | --- |
| `Dim` `DimAligned` `DimRadius` `DimAngle` | dimensions |
| `Text` | model space or layout space — they print differently |
| `Leader` | text with a pointer |
| **`Dot`** | a text dot that always faces you and never scales |
| `Hatch` | needs a closed curve; scale is per-file |

Styles live in *Document Properties ▸ Annotation Styles*. **Set the style once,
per file** — chasing individual dimension sizes is a waste of an afternoon.

**`Dot` is the one you will use most later**: panel numbers in Week 14 are dots,
because they stay readable at any zoom and never rotate.

Keep all of it on `80_DRAWING` so it switches off in one click.

## 3. Layouts

A **layout** is a sheet. On it, **details** are windows into model space.

1. `Layout` — make one, set paper size
2. Double-click **into** a detail to work in it, double-click out to leave
3. Set the **scale** in the detail's properties — `1:50`, `1:100`
4. **Lock the detail** so panning cannot silently change it

> Not locking details is how a drawing set ends up at four different scales
> without anyone noticing.

**Layers can be switched off per detail** — that is how one model produces a
plan *and* a section. Title block and sheet text go in **layout** space.

**Print width** is set per layer and is independent of what you see on screen.
**`PrintDisplay`** shows the real widths before you print. A drawing that looks
right on screen and prints as uniform hairlines is the standard failure, and a
five-second fix if you know.

## 4. Images

**`ViewCaptureToFile`** — captures at a **chosen resolution**, not screen size.
Use it, never the OS screenshot key.

- ask for 3000–4000 px on the long edge
- turn off the **grid** and the **axis icon** for anything anyone else sees
- set the **display mode first**: `Arctic`, `Technical`, `Pen` and `Ghosted`
  give completely different drawings from identical geometry, in one click

`ViewCaptureToClipboard` for a quick paste. `Render` is a further step and
rarely worth it here — a clean `Arctic` capture with good line weights beats a
mediocre render.

## 5. Toward fabrication

| | |
| --- | --- |
| `UnrollSrf` | flattens **developable** surfaces |
| `Squish` | some non-developable cases, with controlled distortion |
| `Contour` `Section` | slicing |
| `Make2D` | the cut geometry, once flat |

**Doubly-curved surfaces will not unroll.** That is geometry, not a bug. The
three honest responses: approximate with planar strips, triangulate, or accept
the distortion and *document how much*.

Laser and CNC want **closed, planar curves**, on known layers, at 1:1.

Week 14 does all of this properly, driven from Grasshopper. This week is so you
know what the target looks like.

---

## Do this before Week 05

1. **One sheet**: plan, one elevation, one section, at a stated scale, with a
   title block, printed to PDF.
2. **One image**: `ViewCaptureToFile`, 2000 px or more, deliberate display mode,
   no grid.
3. **One element unrolled** flat and dimensioned.
4. [Self-check](/SELF-CHECK.md) clean — **this model becomes your project base.**

🎓 **The project brief is released this week.** Read it before Week 05.

## Commands

The commands this week centres on. If one of these is not covered by the prose above, that's a signal to teach it — the list here is the week's source of truth for what students walk in expecting to use.

```
Make2D
Silhouette
Dim
Text
Leader
Dot
Hatch
Layout
PrintDisplay
ViewCaptureToFile
UnrollSrf
Squish
Contour
Section
```
## Reference

- [Drawings, Make2D & Layouts](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/drawings-make2d-layouts)
- [Fabrication Prep](https://kb.rccn.dev/computation/rhino-grasshopper/workflows/fabrication-prep)
- [Figure & Screenshot Style Guide](https://kb.rccn.dev/computation/figure-and-screenshot-style-guide)

---

Previous: [Week 03](/Lecture/Week_03/README.md) · Next: [Week 05](/Lecture/Week_05/README.md) — Grasshopper starts
