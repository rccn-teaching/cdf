# Week 01 — The anatomy of a Rhino model

> **This page is the reference.** The session is a demo; this is what you come
> back to afterwards. Sections match the order we cover them in class.

Rhino knows five or six kinds of thing and one way of describing curved
surfaces. Learn those and the rest of the interface is lookup. Skip them and
you will spend the semester finding workarounds for behaviour that was never
mysterious.

---

## 1. Why Rhino, and not Revit

Revit knows what a wall *is*. That is its strength, and the precise reason it
resists you.

| | Revit | Rhino |
| --- | --- | --- |
| knows about | buildings | geometry |
| gives you | behaviour, schedules, coordination | anything you can describe |
| costs you | anything outside its vocabulary | everything it does for free |

Reach for Rhino when your design is **not one of Revit's nouns**: double
curvature, fast massing, continuous variation across a facade, anything headed
for a machine, or messy inbound survey data.

Do *not* reach for it to coordinate services or hold a model thirty consultants
edit. It will not stop you, which is the danger.

## 2. How you drive Rhino — the command line

Rhino is a **command-line application with a 3D viewport attached**. Everything
is a command; the toolbars are just buttons that type them for you. People who
are fast at Rhino are fast because they stopped using the toolbars.

**Start typing anywhere** — no need to click the command box first. Rhino
autocompletes, and the options appear as clickable words in the command line.

| Key | Does |
| --- | --- |
| <kbd>Enter</kbd> / <kbd>Space</kbd> / right-click | **repeat the last command** — the single biggest time saver |
| <kbd>Esc</kbd> | cancel the current command |
| <kbd>Tab</kbd> | autocomplete the command name |
| <kbd>F1</kbd> | help for the command you are in |
| <kbd>F6</kbd> | show/hide the **camera** widget |
| <kbd>F10</kbd> / <kbd>F11</kbd> | control points on / off |
| <kbd>Ctrl</kbd>+<kbd>Z</kbd> · <kbd>Ctrl</kbd>+<kbd>Y</kbd> | undo · redo |

**Read the command line while a command runs.** It is telling you what it wants
next. Most "Rhino isn't doing anything" moments are a command waiting for input
nobody read.

### Aliases

*Options ▸ Aliases* maps a short string to a command. Set these on day one:

```
l    _Line          j    _Join           sbo  _SelBadObjects
pl   _Polyline      tr   _Trim           se   _ShowEdges
ex   _ExtrudeCrv    bd   _BooleanDifference
c    _Circle        cp   _Copy           w    _What
```

The leading underscore makes an alias work regardless of interface language.
Five aliases you actually use beat fifty you do not.

## 3. What things are — the data types

Everything in a Rhino file is one of these. When something behaves oddly, run
**`What`** before anything else: it reports the type, whether it is valid,
whether it is closed, the degree, and the `u`/`v` domains.

| Type | What it is | Notes |
| --- | --- | --- |
| **Point** | one location | |
| **Curve** | line, arc, circle, or free-form | open or closed |
| **Polyline** | straight segments joined | a degree-1 curve |
| **Polycurve** | several curves joined end to end | mixed types allowed |
| **Surface** | a single NURBS patch | has a `u` and `v` domain |
| **Polysurface** | trimmed surfaces joined along edges | Rhino calls this a *Brep* |
| **Solid** | **a closed polysurface** | not a separate type — see below |
| **Extrusion** | lightweight solid for simple extrusions | behaves subtly differently |
| **Mesh** | faceted: triangles and quads | no curvature, just facets |
| **SubD** | subdivision surface | smooth, editable, organic |

### There is no "solid" type

A solid is **a polysurface that happens to be closed** — every edge shared by
exactly two faces, no gaps. That is the entire meaning of the word in Rhino,
and it is why `Cap` is how most solids actually get made.

### Mesh, briefly

A mesh has no curves in it at all — just vertices and flat faces. It is what a
3D printer and a game engine consume, what a scanner produces, and what Rhino
draws on screen even when the underlying object is NURBS (that is the *render
mesh*, and it is why a smooth surface can look faceted).

You will meet meshes properly in Week 12. For now: **different thing, different
job.** Do not convert without a reason.

## 4. NURBS — what the curve actually is

**N**on-**U**niform **R**ational **B**-**S**pline. Four parts, and only two of
them matter day to day:

- **Control points** — the handles. The curve is *pulled toward* them and
  generally does **not** pass through them, except at the ends. `F10` shows them.
- **Degree** — how far the influence of one control point reaches, and how
  smooth the result is.
  - **degree 1** = a polyline. Straight between points.
  - **degree 3** = the normal smooth curve. Rhino's default, and usually right.
  - higher = smoother and floppier, harder to control locally.
- **Knots** — where each control point's influence begins and ends. The
  *non-uniform* part. You will rarely touch them.
- **Weights** — how hard one point pulls. The *rational* part. Almost never.

> **`Rebuild` is destructive.** It replaces your curve with a new one that
> approximates it at the degree and point count you asked for — useful, and it
> *moves your geometry*. `Refit` changes less. Know which you ran.

## 5. Every surface is a rectangle

**A NURBS surface has four sides. Always.** It is a grid of control points in
two directions, `u` and `v`. It cannot be a triangle, cannot be a disc, cannot
have a hole in it.

So what about the round surface you just made?

**It is a rectangle with most of it hidden.**

### Trimming hides; it does not remove

`Trim` and `Split` do not rebuild the surface. Rhino stores **trim curves** in
`(u, v)` space saying which part to draw. The full rectangular patch — the
**underlying surface** — is still there, in the file.

That one fact explains all of this:

| You see | Because |
| --- | --- |
| `Untrim` "restores" geometry you never drew | it deletes the mask, revealing the rectangle |
| control points sit out in space, off the shape | they belong to the rectangle, not the visible part |
| a `(u,v)` point lands in empty space | that region was trimmed away, but still exists |
| Grasshopper ignores your trims (Week 10) | its surface components work on the rectangle |
| a 1 mm sliver makes a huge file | it still carries the whole original patch |

**`ShrinkTrimmedSrf`** shrinks the underlying rectangle to the smallest one that
still contains the trim. Smaller files, saner `(u,v)`, nothing visible changes.

### Isocurves

The lines running across a surface are **isocurves** — curves of constant `u` or
`v`. Not edges, not geometry: the parameterisation showing through, and the
fastest read you have on surface quality. Even and smoothly flowing = a clean
patch. Bunched or wandering = a surface that will fight you later.

**`Dir`** shows `u`, `v` and the **normal**, which decides which way `OffsetSrf`
goes and which face is "out" at fabrication. **`Flip`** reverses it.

## 6. Join, polysurface, solid

**`Join`** welds edges into a shared boundary. It is a real topological change,
and it only succeeds if the edges are within **tolerance** of each other.

**`Group`** is not the same thing at all — grouping is a selection convenience
and changes no geometry. Two grouped objects are still two objects; two joined
surfaces are one polysurface. Knowing which you have is the difference between a
boolean working and not.

**Naked edges** — `ShowEdges` ▸ *Naked edges* — are edges joined to nothing.
They are the usual, silent reason a boolean fails.

**Bad objects** — `SelBadObjects`, `Check`. A bad object looks completely normal
and will fail to boolean, mesh or export with no useful message. Run
`SelBadObjects` on any file you did not make, before building on it.

## 7. Units and tolerance

`Units` sets both, per file, and both are silent when wrong.

**Absolute tolerance** is how close two things must be before Rhino agrees they
touch:

- **too loose** → things join that are not really aligned; you get polysurfaces
  that look closed and behave as though they are not
- **too tight** for your units → nothing ever joins

**The rule: about 1/1000 of the smallest thing you care about.** Building in
metres → `0.001`. A joint in millimetres → `0.001` mm.

Changing tolerance later does **not** repair geometry already built at the old
one. Set it first, from the template.

> ### When a boolean fails, check in this order
> 1. `SelBadObjects` — is either input invalid?
> 2. `ShowEdges` — is either input actually open?
> 3. `Units` — is tolerance sane for this size?
> 4. Are the two surfaces exactly coincident? Nudge one and retry.
>
> The workaround everyone reaches for — explode, trim, join by hand — produces
> something that *looks* right and is not closed. It fails again later, further
> from the cause.

## 8. Layers, and nesting them

Number them so they sort in **build order** rather than alphabetically —
`10_MASSING` sorts above `20_ENVELOPE`; `Massing` and `Envelope` do not.

```
00_REF          site, surveys, anything you did not draw
10_MASSING      the volumes
20_ENVELOPE     the skin
  21_PANELS       ← nested: drag a layer onto another
  22_FRAME
80_DRAWING      annotation, dimensions, Make2D output
90_TRASH
```

Per layer you control **on/off**, **lock** (visible, not editable — the right
answer for reference geometry you keep clicking by accident), **colour**,
**print width** and **print colour** (independent of what you see on screen),
material and linetype.

**Nested layers**: parent visibility governs children, so the whole envelope
hides in one click.

**Nothing lives on `Default`.** Default is where geometry goes to be forgotten.

## 9. Getting the view you want

**Named views** — `NamedView` saves the current camera and restores it later. Do
this for any view you will capture more than once, or you will never get the
same shot twice.

**`F6`** toggles the **camera widget**, so you can see and drag the camera in a
second viewport. Very few people know it is there.

- **`TwoPointPerspective`** keeps verticals vertical — what architectural images
  almost always want
- **Lens length** in view properties: 50 mm reads naturally, 20 mm is dramatic
  and slightly dishonest
- **`ClippingPlane`** is a live, draggable section — much better than trimming
  repeatedly to see inside
- **Display modes** — `Wireframe`, `Shaded`, `Ghosted`, `Technical`, `Pen`,
  `Arctic`. `Technical` and `Pen` give you a line drawing live in the viewport

### CPlanes

The **construction plane** is the coordinate system you draw on. In Top view it
is world XY; in a perspective view it is whatever you last set.

```
CPlane ▸ Object     align to a face, then draw directly on it
CPlane ▸ 3 Point    define it by picking
CPlane ▸ Save/Restore   name the ones you reuse
Plan                look straight down the current CPlane
```

**`CPlane ▸ Object` then `Plan` is the pairing that matters**: set the CPlane on
a sloped face, look straight down it, and work on that face as though it were
flat.

The **gumball follows the active CPlane** by default. When it points somewhere
unexpected, that is nearly always why.

---

## Do this before Week 02

1. **Set five aliases** you will actually use.
2. **Build one closed solid** — any shape, `Cap`ped, that survives a
   `BooleanUnion` with a second one.
3. **Trim a surface, then `Untrim` it.** Turn control points on first and watch
   where they are. This is the week's idea in one gesture.
4. **Set up your layer structure**, numbered and nested, nothing on `Default`.
5. **Save three named views** and one custom CPlane.
6. Run the [self-check](/SELF-CHECK.md) — eight commands, two minutes.

Bring the file to Week 02. We will run `SelBadObjects` on it and something will
light up.

## Commands

The commands this week centres on. If one of these is not covered by the prose above, that's a signal to teach it — the list here is the week's source of truth for what students walk in expecting to use.

```
What
Line
ExtrudeCrv
Cap
Join
Group
ShowEdges
SelBadObjects
Untrim
ShrinkTrimmedSrf
Dir
Flip
Units
Layer
NamedView
CPlane
Plan
```
## Reference

- [NURBS Anatomy](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/nurbs-anatomy) — the long version of §4–6
- [Geometry & Data Types](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/geometry-data-types) — §3
- [Interface, Navigation & Display](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/interface-navigation-display) — §2, §9
- [Layers & Organization](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/layers-organization) — §8
- [CPlanes & Coordinates](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/cplanes-coordinates) — §9
- [Best Practices](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/best-practices) — §7

---

Next: [Week 02](/Lecture/Week_02/README.md)
