# Week 04 — Getting it out

> **This page is the reference.** Last Rhino week — Grasshopper starts next.

A model is not finished when it looks right. It is finished when something
**true** can be extracted from it: a drawing at a stated scale, an image, or a
cut file a machine will accept.

Everything below assumes a NURBS model, so start with the case where it is not.

**And know where Rhino stops.** Rhino is a *fast drafting tool* and a
*fabrication tool*. It is not BIM, and it is not a page-layout application.
Most of the time people lose in Rhino is spent trying to make it be one of
those:

| | |
| --- | --- |
| **Rhino** | drawing straight off the model you already built · cut files, unrolls, setting-out · a sheet good enough to think with and to hand to a workshop |
| **Revit / ArchiCAD** | schedules, coordination, a model several people edit at once |
| **Illustrator / Affinity / InDesign** | the final graphic pass — fills, texture, type, the portfolio board |

The pipeline this course actually runs is **Rhino → vector PDF → Illustrator or
Affinity**, and the whole reason it works is §6: get the layers and pens right
on the way out and the graphic pass takes twenty minutes instead of an evening.
Rhino's job is to be **true**. Making it beautiful is a different tool's job,
and handing over cleanly is a skill in itself.

---

## 1. SubD, and when it is the wrong answer

Week 01 listed **SubD** as one of Rhino's data types and left it there. Here is
the rest.

A SubD is a **coarse cage of quad faces** that Rhino smooths. You drag a handful
of cage points and a continuous surface follows. No degree, no knots, no U/V
trim mask — none of the NURBS anatomy applies. `Tab` (or
`SubDDisplayToggle`) flips between the smooth result and the box cage;
`SubDCrease` pins an edge sharp.

**Use it to find a form.** Canopies, shells, furniture, a competition massing —
anything where the shape is still the question and no dimension is fixed.
Sculpting a doubly-curved roof in SubD takes minutes. Building the same shape
from NURBS curves takes an afternoon and fights you the whole way.

**Stop using it the moment the drawing matters.** Not because SubD is bad, but
because the rest of this page asks for things it does not have:

| what output needs | what a SubD gives you |
| --- | --- |
| a dimension you can put on a sheet | a cage position — the surface is *near* it, not on it |
| edges with structure behind them | edges wherever the cage happened to fall |
| `UnrollSrf`, `Contour`, `Section` | nothing, until you convert |
| a Grasshopper definition from Week 05 on | a data type most of this course's components do not take |

`ToNURBS` converts, and the conversion is the trap: **every quad face of the
cage becomes its own untrimmed NURBS patch.** A twenty-face SubD becomes a
twenty-patch polysurface whose seams sit where the cage sat — not where your
structure, your panels or your cut lines want them. It is watertight, and it is
useless to draft from.

**So rebuild, do not convert.** Sculpt in SubD, take sections or a curve network
through the shape you like, and loft or `NetworkSrf` a NURBS surface through
*those*. Now the seams are where you put them. Or keep both: the SubD for the
image, the rebuilt NURBS for the drawing and the cut file.

> If a doubly-curved SubD form is the centre of your project, decide **now** how
> it gets built — §8 is the constraint, and Week 14 will not rescue you from it.

## 2. `Make2D`

Projects 3D geometry into 2D curves, from the current view or a named one. Run
it once per drawing: `Top` for a plan, `Front` or `Right` for an elevation, and
either of those with a `ClippingPlane` in place for a section. The output lands
flat on world XY beside the model, so it only reads properly in `Top`.

**The options that matter**, in the order they bite:

| option | why |
| --- | --- |
| **Maintain source layers** | the most important checkbox on the dialog — see below |
| **Layer name** | sets the *parent* layer of the output; point it at `80_DRAWING` and skip the tidying |
| **Clipping plane intersections** | your cut line, on its own sublayer |
| **Tangent edges** | the lines where a fillet rolls away |
| **Register with previous** | keeps a new drawing in the same registration as the last one |
| **Viewport rectangle** | a frame at the viewport edge; perspective views only |

**Maintain source layers** mirrors your model's layer tree underneath the
output, so `12_Wall` comes out as a wall layer and `14_Glass` as a glass one.
Without it every line lands in one undifferentiated pile and you cannot give
walls a heavier pen than glass — which is the whole of §6. Tick it every time.

```
80_DRAWING
  visible lines
    12_Wall
    13_Floor
    14_Glass
  clipping planes
    12_Wall
    …
```

Three more things about `Make2D`:

- **Tangent edges on** is the honest default for a technical drawing; turning
  them *off* is often what makes a presentation drawing read. Look at both
  before you choose.
- **Slow on heavy models.** Hide what you do not need first.
- **Static.** Change the model, run it again — there is no link.

**`Silhouette`** gives just the outline of an object, live and much faster. For
a massing diagram or a figure-ground it is usually the better tool.

## 3. Live sections, and why they usually beat `Make2D`

`Make2D` is the old road and you should know it, because it is the only thing
that gives you a full hidden-line drawing. But for the plan and section you
will redraw eleven times between now and Week 18, Rhino 8 has something better,
and it is the strongest argument for drafting in Rhino at all.

**`ClippingSections`** makes a clipping plane built for drafting rather than for
looking: it takes a direction and a depth, it gets a **name and a label**, and
it can be saved straight to Named Views so *plan at +1.2 m* is one click away
for the rest of the project.

**Section styles** are the part that changes what a drawing looks like. A
section style — set **per layer**, and that is how to set it — carries a
**hatch pattern, a fill and a boundary**: pattern, scale, rotation, boundary
colour and boundary width. Put a concrete hatch on `12_Wall` and every wall the
plane cuts is poched, everywhere, forever, with no hatching by hand.

| | |
| --- | --- |
| `ClippingSections` | the drafting clipping plane — direction, depth, name, label |
| `ClippingDrawings` | extracts the section plus background geometry as 2D on world XY |
| `UpdateClippingDrawings` | pulls the model's changes through |
| `ExtractClippingSections` | the cut curves and hatches, in place, as real geometry |
| `ViewClippingSections` | which viewports a section is allowed to cut |

**And it is not static.** Move the plane, or change the building, and
`UpdateClippingDrawings` brings the drawing with it. That one difference is
what makes it worth setting up: `Make2D` is a photograph, a clipping drawing is
a view.

> **Cut a section, drag the plane, watch the poché follow.** If you take one
> habit out of this week, take that one.

**A material legend** falls out for free: a row of small hatched circles using
the same section styles, labelled, in the corner of the sheet. It costs five
minutes and it is the difference between a drawing and a diagram.

**When to fall back to `Make2D`**: full hidden-line work, elevations of things a
clipping plane cannot describe, and anything you are about to hand to a machine.

## 4. Layouts and details

A **layout** is a sheet. On it, **details** are windows into model space.

### Making the sheet

The `+` beside the viewport tabs ▸ **New Layout**. Four decisions, all
changeable afterwards from right-click ▸ *Layout Properties*:

- **name** — `A1-01`, not `Layout 01`
- **printer** — set it to **Rhino PDF** now; it is what makes the paper size real
- **size and orientation** — A1 landscape for this course
- **initial detail count** — one is fine, add the rest as you go

### Being in the right place

**Double-click inside a detail to go into model space; double-click outside to
come back out.** Almost everything confusing about layouts is this one gesture.

- inside, the detail border darkens and you are navigating the **model**
- outside, zooming zooms the **sheet**
- the viewport title bar tells you which — read it before you blame Rhino

### Scale

Select the detail ▸ Properties ▸ **Scale**. Rhino states it as *N mm on the page
= M units in the model*, which is not a ratio, and it trips everyone. Work it
out from one unit. In a **metre** file:

| page | model | scale |
| --- | --- | --- |
| 1 mm | 1 | 1:1000 |
| 10 mm | 1 | **1:100** |
| 20 mm | 1 | **1:50** |
| 50 mm | 1 | 1:20 |

Then **lock the detail**. Zooming inside an unlocked detail silently changes its
scale — and if you panned around hunting for the section, you have already
broken it. Set the scale, lock, do not touch it again.

> Not locking details is how a drawing set ends up at four different scales
> without anyone noticing.

### More details, and lining them up

Add one from the **Layout** toolbar, or — better — **copy a detail you have
already scaled**, because the copy carries its scale with it. Copy, double-click
in, right-drag to pan to the next drawing, **re-check the scale**, double-click
out.

To align plan, elevation and section: from layout space select the whole
**detail frame**, `Move`, and **snap a feature in one drawing onto the matching
feature in the next** — a wall end, a grid line, a corner. Then slide the frame
along one axis only with the gumball to separate them. Everything stays
projected.

### One model, many drawings

Two things are set **per detail**, and between them they are how one model gives
you a whole drawing set:

- **layers** switch off per detail — plan and section from the same geometry
- **clipping** is per detail too. `ViewClippingSections`, or the *Views clipped*
  property on the plane, says which details a given section is allowed to cut.
  Without it your plan cut shows up in the elevation.

Title block, sheet text and the frame belong in **layout** space, not inside a
detail.

### The title block

Make it a **block** — the Week 03 argument, cashed in. `BlockEdit` it once and
every sheet in the set updates; leave it as loose lines and you will be editing
nine of them by hand in Week 18.

Inside it, use **text fields** rather than typed text: *PageName*, *PageNumber*,
the date, the file name. They fill themselves in per sheet, so one block serves
the whole set and nothing says `A1-03` on sheet four.

## 5. Annotation

| | |
| --- | --- |
| `Dim` `DimAligned` `DimRadius` `DimAngle` | dimensions — `DimAligned` is the workhorse |
| `Text` | model space or layout space — they print differently |
| `Leader` | text with a pointer |
| **`Dot`** | a text dot that always faces you and never scales |
| `Hatch` | needs a closed curve; scale is per-file |

Styles live in *Document Properties ▸ Annotation Styles*. **Set the style once,
per file** — chasing individual dimension sizes is a waste of an afternoon. What
is worth setting on the way past:

- **font, text height, arrowhead type and size** — the defaults are for
  engineering drawings on A4
- **length units and decimal places** — the default often reads `12000.001`
  where you wanted `12000`. Set decimal places to 0 and round.

Edit the style afterwards and **every dimension in the file updates**. That is
the whole reason to use styles rather than fix things one at a time.

**Leaders**: make one, get its angle right, then **copy it** for the next
callout and rename the text. All your leaders at one angle is most of what makes
a sheet look deliberate. To tidy a set you have already made, `SelLeader` (and
`SelDim` for dimensions) grabs every one of them at once, and the gumball will
line their control points up to a common height.

**`Dot` is the one you will use most later**: panel numbers in Week 14 are dots,
because they stay readable at any zoom and never rotate.

## 6. Print colour, print width, and the PDF

This is where a drawing stops looking like a screenshot.

**Both are set per layer, in the Layers panel, and both are independent of what
you see on screen.** That is why §2's *Maintain source layers* mattered: the
mirrored model tree is the thing you hang pens on.

**`PrintDisplay` must be on or you are working blind.** It is **off by
default** — type `PrintDisplay`, set *State* to **On**, Enter. Without it you
will change a print colour, see nothing happen, and change it again.

> Print colour shows in **layout** space. In model space you still see the layer
> colour. That is correct, not a bug.

A workable set of pens — the numbers are **millimetres on the paper**:

| | |
| --- | --- |
| cut line (clipping plane) | 0.50, darkest colour |
| ground, massing | 0.50 |
| walls, structure | 0.30 |
| secondary elements | 0.18 |
| glass, fine detail | 0.13 |

For colour, a **tonal family** reads better than black on white — pale blue for
the seen lines, a dark blue for the cut, grey for the frame and annotation.
Black is a choice, not a default.

**Linetypes** are per layer too. Draw the line solid, move it to a dashed layer,
set *Linetype* there. New patterns come from **File ▸ Properties ▸ Linetypes ▸
Add**, where the pattern is dash length then gap length in millimetres — `2,2`,
`5,5`, `1,1`. Dashed lines dropped between a plan and a section to carry a
height across are cheap and do a lot of work.

**A layer that does not print.** Set a layer's print width to **No Print** and
put detail frames, construction rectangles and setting-out lines on it. They
stay visible while you work and vanish from the PDF.

```
80_DRAWING
  visible lines / clipping planes   ← the Make2D mirror; pens live here
  81_ANNOTATION                     grey
  82_FRAME                          grey, 0.13
  83_DASHED                         dashed linetype
  89_GUIDES                         No Print
```

### Out to PDF

**File ▸ Print.** Four settings, and three of them are wrong by default:

| | |
| --- | --- |
| **Destination** | Rhino PDF |
| **Size / orientation** | the same as the layout — check, do not assume |
| **Output type** | **Vector** |
| **Output colour** | **Print colour** — otherwise every pen you just set is ignored |

Then save as PDF — on macOS that is the *Save as PDF* button at the bottom of
the print dialog. Printing the whole set at once is the **Multiple layouts**
option, at 1:1 — the scale is already in the details.

A drawing that looks right on screen and prints as uniform grey hairlines is the
standard failure of this week, and a five-second fix if you know where to look.

**Why vector matters beyond the print.** A vector PDF opens in Illustrator or
Affinity with every line still an editable path at the width you set. You can
restyle it; you never have to redraw it. A raster PDF is a photograph of a
drawing. One dropdown is the difference between a twenty-minute graphic pass
and an evening of tracing — which is the whole argument of the table at the top
of this page.

## 7. Images

**`ViewCaptureToFile`** — captures at a **chosen resolution**, not screen size.
Use it, never the OS screenshot key.

- ask for 3000–4000 px on the long edge
- turn off the **grid** and the **axis icon** for anything anyone else sees
- set the **display mode first**: `Arctic`, `Technical`, `Pen` and `Ghosted`
  give completely different drawings from identical geometry, in one click

`ViewCaptureToClipboard` for a quick paste. `Render` is a further step and
rarely worth it here — a clean `Arctic` capture with good line weights beats a
mediocre render.

## 8. Toward fabrication

| | |
| --- | --- |
| `UnrollSrf` | flattens **developable** surfaces |
| `Squish` | some non-developable cases, with controlled distortion |
| `Contour` `Section` | slicing |
| `Make2D` | the cut geometry, once flat |

**Doubly-curved surfaces will not unroll.** That is geometry, not a bug. The
three honest responses: approximate with planar strips, triangulate, or accept
the distortion and *document how much*. This is the bill that §1 warned you
about.

Laser and CNC want **closed, planar curves**, on known layers, at 1:1. Select
just those curves and `Export` them to `.dxf` — layer names survive, and layer
names are how the machine is told what to cut, what to score and what to
ignore. Check the units in the export scheme before you walk to the workshop.

Week 14 does all of this properly, driven from Grasshopper. This week is so you
know what the target looks like.

---

## Do this before Week 05

1. **One sheet**: plan, one elevation, one section, at a stated scale, details
   locked, pens set with `PrintDisplay` on, title block, printed to PDF as
   **vector**.
2. **One image**: `ViewCaptureToFile`, 2000 px or more, deliberate display mode,
   no grid.
3. **One element unrolled** flat and dimensioned.
4. [Self-check](/SELF-CHECK.md) clean — **this model becomes your project base.**

🎓 **The project brief is released this week.** Read it before Week 05.

## Commands

The commands this week centres on. If one of these is not covered by the prose above, that's a signal to teach it — the list here is the week's source of truth for what students walk in expecting to use.

```
SubDDisplayToggle
SubDCrease
ToNURBS
Make2D
ClippingPlane
Silhouette
ClippingSections
ClippingDrawings
UpdateClippingDrawings
ExtractClippingSections
ViewClippingSections
Layout
BlockEdit
PrintDisplay
Print
Dim
DimAligned
Text
Leader
Dot
Hatch
SelDim
SelLeader
ViewCaptureToFile
UnrollSrf
Squish
Contour
Section
Export
```
## Reference

- [Geometry Data Types](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/geometry-data-types) — where SubD sits among the rest
- [Drawings, Make2D & Layouts](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/drawings-make2d-layouts)
- [Fabrication Prep](https://kb.rccn.dev/computation/rhino-grasshopper/workflows/fabrication-prep)
- [Figure & Screenshot Style Guide](https://kb.rccn.dev/computation/figure-and-screenshot-style-guide)
- [Layout Pages in Rhino](https://www.youtube.com/watch?v=CdnD4dJ3MTI) — Tom Budd, 20 min; §4–§6 as a screencast
- [Drafting: Architecture](https://www.rhino3d.com/docs/guides/user-guide/drafting-architecture/) — McNeel's own §3 walkthrough, in full, with sample files

---

Previous: [Week 03](/Lecture/Week_03/README.md) · Next: [Week 05](/Lecture/Week_05/README.md) — Grasshopper starts
