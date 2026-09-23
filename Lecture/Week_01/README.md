# Week 01 — The anatomy of a Rhino model

> **This page is the reference.** The session is a demo; this is what you come
> back to afterwards. Sections match the order we cover them in class.

Rhino knows five or six kinds of thing and one way of describing curved
surfaces. Learn those and the rest of the interface is lookup. Skip them and
you will spend the semester finding workarounds for behaviour that was never
mysterious.

**The four-week arc you are entering:**

| Week | You leave able to… |
| --- | --- |
| **01 · this week** | navigate Rhino, name the objects it makes, model one closed solid |
| **02 · next week** | draw clean curves and lift them into surfaces — the making step |
| **03** | work at scale — selection, blocks, model hygiene, references |
| **04** | get it out — plans, sections, elevations, dimensions, layouts, PDFs — the **drafting and detailing** week |

By the end of W04 you can rapid-mass an idea, refine it, and produce a
drawing set. By the end of W15, that same model drives Grasshopper.

---

## 0. First fifteen minutes — getting Rhino to move

**Never opened Rhino before? Start here.** The rest of the page assumes you
can see the four viewports, orbit them with the mouse, click on an object,
and press `Ctrl+S`. If any of that is new, spend fifteen minutes on this
section before the rest.

### 0.1 The four viewports

When you open a new file, the screen is split into four windows:

| | Shows | Reads as |
| --- | --- | --- |
| **Top** (upper-left) | looking straight down | your **plan** |
| **Front** (lower-left) | looking north from the south | your **elevation** |
| **Right** (lower-right) | looking west from the east | a **section** |
| **Perspective** (upper-right) | 3D view | how the thing actually looks |

**Double-click a viewport title** to maximise it; double-click again to
un-maximise. Everything you do in one viewport appears in all four
simultaneously — that is how you check what you drew looks right from every
side.

Architecturally: **Top is where you draft, Perspective is where you check,
Front and Right are where you notice something is at the wrong height.**

### 0.2 Move the view with the mouse

You are always doing one of three things when you are not running a command:

| Mouse action | Does |
| --- | --- |
| **Right-drag** (or RMB-drag) | **orbit** in Perspective, **pan** in the parallel viewports |
| **Shift + right-drag** | **pan** in every viewport (including Perspective) |
| **Scroll wheel** | **zoom** at the cursor |
| **Left-click** | **select** an object |
| **Left-click empty space then drag** | **selection window** (left→right = fully-inside; right→left = anything-it-touches — see W03) |

**`ZE`** (`ZoomExtents`) zooms the current viewport to fit everything;
**`ZEA`** does it in all four viewports at once. If the view feels broken —
you cannot find what you drew, the target is stuck in space — `ZEA` is the
reset. Learn it as a reflex now.

### 0.3 Draw your first thing, look at it, save

Six commands, in order. Type each one; do not hunt for it in a toolbar.

```
Rectangle          two clicks — one corner, then the opposite corner
                   (or: type dimensions, e.g., `10<Enter>5<Enter>` for 10×5)
ExtrudeCrv         click the rectangle, type 3<Enter>  →  a 10×5×3 mass
ZEA                zoom every viewport to it
NamedView          save this Perspective view as "hero"
Ctrl+S             save the file — Rhino uses .3dm; give it a real name, not a number
Ctrl+Z             undo — the reflex for "wait, no"
```

That is the **rapid-massing loop** in six commands: draw a footprint,
extrude, look at it, save. From here everything is refinement — walls
become `PolySrf`s, the roof becomes an angled surface, an opening becomes
a `BooleanDifference` with another box. Same six commands underneath.

### 0.4 The habits that make everything faster

Three keys and one habit that pay off for the rest of the term:

- <kbd>Enter</kbd> / <kbd>Space</kbd> / right-click on empty space
  = **repeat the last command**. Draw ten walls without retyping `Line`.
- <kbd>Esc</kbd> = **cancel** the current command. You will need this
  constantly. Look up when confused; the command line will tell you what
  Rhino is waiting for.
- <kbd>F1</kbd> = **help on the command you are in the middle of**.
  Better than any web search, especially for command options.
- **`Ctrl+S` every five minutes.** Rhino crashes. Not often, but every
  student loses at least one afternoon of unsaved work per term.

That is the whole beginner surface. The rest of this page unpacks what
each of those commands actually did and why.

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


## 2. How you drive Rhino — the command line

Rhino is a **command-line application with a 3D viewport attached**. Everything
is a command; the toolbars are just buttons that type them for you. People who
are fast at Rhino are fast because they stopped using the toolbars.

**Start typing anywhere** — no need to click the command box first. Rhino
autocompletes, and the options appear as clickable words in the command line.

| Key | Does |
| --- | --- |
| <kbd>Enter</kbd> / <kbd>Space</kbd> / right-click | **repeat the last command** — the single biggest time saver |
| <kbd>Tab</kbd> | autocomplete the command name |
| <kbd>F6</kbd> | show/hide the **camera** widget |
| <kbd>F10</kbd> / <kbd>F11</kbd> | control points on / off |

**Read the command line while a command runs.** It is telling you what it wants
next.

**Command options have hotkeys too.** While a command is running, each option
in the prompt has a letter shown as its shortcut — press it instead of
clicking. `Rotate` ▸ *Copy* is `C`; `Move` ▸ *Vertical* is `V`. Small effort,
big saving.

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

Aliases can also run **macros** — a chain of commands with typed input,
useful for repetitive setups. Check the Rhino help under *Aliases* for the
macro syntax when you need it.

## Modelling aids

Three things live outside a command but change how every command behaves.
Turn each one on for the section of the model where it helps and off when
it stops helping — none of them are meant to be always on.

### The gumball

Toggle with the icon in the status bar (or `Gumball`). Click a handle to
drag; **type a distance** while dragging to move exactly that far; hold
<kbd>Alt</kbd> while dragging to **copy** instead of move. It follows the
active CPlane (§9), which is why setting a CPlane first is often the
difference between a natural drag and a wrong one.

### Object snaps

**Osnaps** — `End`, `Mid`, `Cen`, `Int`, `Perp`, `Tan`, `Quad`, `Near`,
`Node`, `Point` — sit in a bar at the bottom and are persistent. **Turn on
only what you need**; every osnap on at once means several compete for
the same click and you pick the wrong one silently.

**`Project` on the osnap bar** is the trap: it forces every snapped point
onto the CPlane. Either exactly what you want (drawing plans), or the
reason everything landed at `z = 0` when you meant to snap in 3D. Know
which state it is in.

### Angle snap and Ortho

**`Ortho`** (hold <kbd>Shift</kbd>) constrains movement to the CPlane axes.
**Angle snap** — *Options ▸ Modeling Aids ▸ Snap* — snaps rotations to a
fixed increment; toggle with the *Snap* checkbox in the status bar and
change the increment where you set it. Same for **grid snap** (<kbd>F9</kbd>).

**`SmartTrack`** shows temporary reference lines off snapped points — good
for lining up something with two things at once without drawing a
construction line first.

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

**`Explode` a solid, then `Join` again**, and watch the reported type change
in `What`: an `Extrusion` becomes a `Polysurface` becomes a `Closed
polysurface` once every edge is shared. Same shape on screen — but the name
is what `Cap`, the booleans, mesh, and export operations actually key on.

### Mesh

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

Layers **nest** — drag one onto another to make it a child. Build the
hierarchy the way your workflow reads. Number the top level if you need it
to sort in a specific order; otherwise layers sort alphabetically.

```
00_REF          site, surveys, anything you did not draw
10_1F
  11_Column
  12_Wall
  13_Floor
20_2F
  21_Column
  22_Wall
  23_Floor
```

Per layer you control **on/off**, **lock** (visible, not editable — the right
answer for reference geometry you keep clicking by accident), **colour**,
**print width** and **print colour** (independent of what you see on screen),
material and linetype.

**Parent visibility governs children.** Hiding `10_1F` hides everything under
it in one click.

**Nothing lives on `Default`.** Default is where geometry goes to be forgotten.

**Layer states** (`LayerStateManager`) save the whole on/off/lock/colour
configuration under a name — one state for *1F only*, one for *2F only*, one
for *structure only*. Switching stops being ten clicks per view; it becomes
one. Save them as you find them.

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

**Camera target.** The **target** is the point the view orbits around. Lose
track of it — pan far, orbit strangely — and further navigation feels
broken. `ZS` (`ZoomSelected`) puts the target on whatever is selected in the
current view; `ZSA` (`ZoomSelectedAllViewports`) does it in every viewport
at once. Fast reset.

### CPlanes

The **construction plane** is the coordinate system you draw on. In Top view
it is world XY; in a perspective view it is whatever you last set.

**One CPlane per floor's base reference point.** Rather than copying a floor
plan to `z = 0` to work on it, leave the plan where it belongs in the model
and set a CPlane whose origin is that floor's reference. Draw, snap and
project on that CPlane; the floor stays as the single source of truth. This
matters most on sites where each floor has a different datum — the moment
you copy plans around to work at `z = 0`, that reference is lost.

Elevations get their own CPlanes too. Anything on an awkward angle — a
tilted roof, an angled facet — is easier to draw on once a CPlane is
aligned to it.

```
CPlane ▸ Object          align to a face, then draw directly on it
CPlane ▸ 3 Point         define it by picking three points
CPlane ▸ Save/Restore    name the ones you reuse
Plan                     look straight down the current CPlane
```

**Combine `NamedView` + `LayerState` + a saved `CPlane`** and you have a
named working environment — *"1F structural plan"*, *"north elevation
detail"*, *"the tilted roof"*. Two clicks to enter one, two clicks to leave.

**`CPlane ▸ Object` then `Plan`** is the pairing that matters: align the
CPlane to a face, look straight down it, and work as though it were flat.

The **gumball follows the active CPlane** by default. When it points somewhere
unexpected, that is nearly always why.

### This is a production workflow — use it when it earns its keep

Numbered floors, per-floor CPlanes, saved layer states, named environments —
this pays off when the model is *going somewhere*. Coordination, fabrication,
a hand-off, a second person driving it, a Grasshopper definition referencing
it by name from Week 05. That is when the discipline is worth the setup.

**Rhino is still a rapid prototyping tool**, and that is its other superpower.
Early massing, quick tests, form-finding, an idea you might throw away in
five minutes — do those on flat layers, at world coordinates, with the
gumball on whatever plane it lands on. There is nothing to organise yet, and
the ceremony would slow you down.

The failure mode is not the one students expect. It is not sloppy files; it
is files so carefully organised that the designer stops *trying things*.
**Keep the sketch fast.** Move to the structure above when the design has
decided what it is, not before — and expect to keep an "experiment" layer or
a `99_SCRATCH` even in an organised file, for the next idea you want to
test loosely.

---

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
