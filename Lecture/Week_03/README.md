# Week 03 — Working at scale

> **This page is the reference.** Unglamorous, and the week that decides whether
> Week 14 is possible.

A model you cannot navigate is a model you cannot finish. Everything here is
about **finding, changing and reusing** — the things that stop mattering at
ten objects and decide everything at ten thousand.

Two shapes to the week:
**sections 1-2** are how you *move and rework* what you found without rebuilding;
**section 3** is how you *find* what you mean; 
**sections 4–8** are how the model stays legible when a lot of that has accumulated.

---

## 1. Transformations — moving what you already have

Once you can select, the next thing you do is move it. The pattern is the
same for every transform: **pick objects → answer a base point → answer a
target**. Two habits pay off from day one — **type distances** rather than
snapping to a rough spot, and **use the `Copy` option** built into every
transform command rather than duplicating first and moving after.

| Command | Does | Precision input |
| --- | --- | --- |
| `Move` | translation | after base point, type a distance or an XYZ vector |
| `Copy` | move that duplicates | same, and it repeats until <kbd>Enter</kbd> |
| `Rotate` | rotation around a point | type an angle after picking the reference |
| `Rotate3D` | rotation around an axis | pick two points to define the axis |
| `Scale` `Scale1D` `Scale2D` | uniform / one-axis / two-axis scaling | type a factor, or two reference distances |
| `Mirror` | reflect across a line | in Front/Top a single point + axis is enough |
| `Align` | to edge or centre, one axis at a time | pick axis and side |
| `Distribute` | even spacing across a selection | one axis, no numeric input needed |
| `Divide` | split a line or curve into equal segments | pick the start and end, then type a count |
| `SetPt` | force chosen coordinates to a single value | set the Z of many points at once |

### The `Copy` option is on every transform

Inside a running `Move`, `Rotate`, `RotateAxis`, `Scale`, `Mirror`, `Rotate3D`
and friends, the prompt exposes a **`Copy=No/Yes`** option — toggle it once
with the letter `C` or by clicking the word, and the transform leaves the
original in place. This is faster and more precise than a separate `Copy`
step, and it removes the classic mistake of moving what you meant to
duplicate.

**Repeat the last transform with the same numbers** — press <kbd>Enter</kbd>
after a `Move` to re-run it. Combined with `SelLast` this is how you
stack fifteen slabs at exact 3 m centres without touching the mouse.

### Orient — align by picking, not by typing

The `Orient` family moves *and* rotates *and* (optionally) scales in one
gesture, by picking reference points on the source and matching them to
points on the target.

| Command | Use when |
| --- | --- |
| `Orient` (2-point) | you want to align two known points on the source to two on the target |
| `Orient3Pt` | you need to lock a whole plane — moving object stays coplanar with the target |
| `OrientOnSrf` | dropping objects onto a surface at picked (u,v) points, using the surface normal |
| `OrientOnCrv` | placing along a curve at picked parameters, using the curve's tangent |
| `RemapCPlane` | move objects between CPlanes — the workflow companion to your W01 floor CPlanes |

**`OrientOnSrf` is the command students never guess exists** — it is how
you scatter panels, mullions, or vegetation onto a curved facade without
scripting a single line.

### Arrays — controlled repetition

| Command | Repeats along |
| --- | --- |
| `ArrayLinear` | a straight line, given count + spacing |
| `ArrayPolar` | a circle, given count + total angle |
| `ArrayCrv` | a curve, oriented to the curve's tangent |
| `ArraySrf` | a surface, in (u,v), oriented to the normal |

Arrays are one-shot in Rhino (edit means delete-and-redo). If the pattern
is going to change often, do it in Grasshopper — from Week 05 on.

### Gumball vs a command

The gumball is faster for anything **rough**: nudge, rotate a hair, scale
by eye. A command is better for anything **precise** or anything you will
need to **repeat**. As a rule: if you would type a number, use the command.
If you would eyeball it, use the gumball.

The gumball also has its own numeric input — click a handle, start
dragging, and type — but it does not surface the `Copy` option the way a
transform command does. Hold <kbd>Alt</kbd> while dragging a gumball
handle to copy instead of move.

## 3. Modifications — reworking what you already have

Modelling is 20% making and 80% fixing what you made. These are the
commands that turn "the geometry is nearly right" into "the geometry is
what I want" without rebuilding from scratch. Grouped by what they let
you *pull off* an object, *change on it in place*, or *reconcile* between
objects.

### 3.1 Extracting — pulling curves or sub-parts off geometry

Every polysurface has edges, faces, and an underlying construction you
can borrow from. These commands make those borrowable without disturbing
the original.

| Command | Extracts | Why you reach for it |
| --- | --- | --- |
| **`DupEdge`** | one edge → a curve | outline a face for `Make2D`, feed a curve to Grasshopper, project onto a surface |
| **`DupBorder`** | the full outer border → a closed curve | fastest way to get "the shape of this thing" as a curve |
| **`DupFaceBorder`** | the border of one face → a closed curve | same, but per face; the panelisation workflow |
| **`ExtractSrf`** | one face → a standalone surface | modify it in isolation, then `Join` it back |
| **`ExtractIsocurve`** | a `u` or `v` curve on a surface | build ribs, rails, panel divisions |
| **`ExtractControlPolygon`** | the control net → curves | when you need to see the underlying NURBS structure |
| **`Silhouette`** | the outline of a solid from the current view | image work, shadow curves, W04 make2d preparation |
| **`Intersect`** | the intersection of two objects → curves | sections, contours, where things cross |
| **`Contour`** | parallel section curves through a solid | floor plans off a mass, terraces, contour drawings |

**`DupEdge` and `DupBorder` are the two most-used commands you don't know
about yet.** Anywhere you would think "I need a curve *just like* this
edge" — panel numbering, laser cutting, Grasshopper input, offset paths —
this is the command. Original geometry is untouched; the new curve lives
on the current layer.

### 3.2 In-place edits — changing what is there

These modify the object rather than making a copy.

| Command | Changes | Notes |
| --- | --- | --- |
| **`ExtractSrf`** with *Copy=No* | pulls a face off, no copy | for isolate-modify-rejoin |
| **`FilletEdge`** `ChamferEdge` | round or cut an edge in place | Week 02 preview — the failure modes are the same |
| **`OffsetSrf`** | thicken a surface into a solid, or offset its face | walls from a slab, cladding from a shell |
| ## `ExtendCrv` | grow a curve past its current end | when a trim was too aggressive |
| **`ExtendSrf`** | grow a surface past its current edge | when a trim was too aggressive |
| **`RemoveEdge`** | dissolve a shared edge between two coplanar faces | opposite of `ExtractSrf`; keeps the polysurface intact |
| **`MergeAllFaces`** | fuse every set of coplanar faces on a polysurface | the *cleanup* command — after booleans that leave twenty tiny faces where one flat panel belongs |
| **`MergeSrf`** | join two open surfaces edge-to-edge into one | when a shell is really one surface in two pieces |
| **`Untrim`** | expose the underlying rectangular patch | Week 01 mask; useful when the visible cut is wrong |
| **`PushPull`** | move a surface along its normal | When you comes from SketchUp |


### 3.3 The extract → modify → rejoin loop

The pattern that solves 80% of "how do I change one bit of this thing"
questions:

```
1.  ExtractSrf         pull the face out of the polysurface
2.  edit it            trim, rebuild, offset, retexture, whatever
3.  Join               weld it back into the polysurface
4.  What               confirm it is Closed polysurface again, not Polysurface
```

This is safer than trying to edit the face in place. It also teaches the
right mental model: a polysurface is a set of surfaces held together by
matching edges — separate one, work on it, reconnect.

### 3.4 Merging — the opposite of the same problem

After a boolean or a repeated `Split`, a face that reads as one flat wall
is often five coplanar triangles internally. These modifications look
identical on screen but behave differently: the split version explodes
into pieces on `Explode`, breaks a face-per-panel workflow, and inflates
Grasshopper trees.

**Run `MergeAllFaces` on any polysurface that has been through booleans.**
It is fast, non-destructive (if nothing merges, nothing changes), and
turns twenty invisible internal edges back into the one face they should
have been.

**`RemoveEdge` is the manual version** — pick the edge you want gone.
Use it when `MergeAllFaces` refuses because the two faces are close to
coplanar but not quite (a floating-point residue from a boolean).

> **The failure mode of this section.** These commands are so useful that
> students reach for them before understanding what a polysurface *is* —
> the answer to "why did my boolean fail" is almost never
> `RemoveEdge`; it is usually a naked edge or an out-of-tolerance join
> (Week 01 §7). Fix the cause, then use these tools for the cleanup.

## 3. Selecting what you mean

Clicking is the slow way. The `Sel*` family is the fast way.

| Command | Selects |
| --- | --- |
| `SelLayer` | everything on a layer |
| `SelName` | everything with a given object name |
| **`SelDup`** | duplicates sitting exactly on top of each other |
| `SelBadObjects` | invalid geometry |
| `SelCrv` `SelSrf` `SelPolysrf` `SelMesh` | by type |
| `SelClosedCrv` `SelOpenCrv` | by state |
| `SelLast` `SelPrev` | what you just made, or just had selected |
| `Invert` | everything else |
| `SelAll` `SelNone` | |

**`SelDup` is the one to run periodically.** Two identical objects look like
one, break booleans, double a panel schedule, and stay invisible until they cost
you.

### Window vs crossing

- **Left → right**: takes only what is **fully inside** the box
- **Right → left**: takes anything the box **touches**

Most people use one of these their whole life without noticing the other exists.

**`SelectionFilter`** restricts what is selectable at all — invaluable when
picking curves out of a dense model.

## 4. Naming, and why it pays later

`Properties` ▸ Name, or `SetObjectName`. A named object can be found with
`SelName`, and — the part that matters — **referenced by name from Grasshopper**
from Week 05 onward.

Name the things a definition will need to grab. Not everything.

## 5. Blocks

A **block** is one definition placed many times. Edit the definition, every
instance updates.

| Command | Does |
| --- | --- |
| `Block` | make a definition from selected geometry |
| `Insert` | place an instance |
| `BlockEdit` | edit the definition in place |
| `BlockManager` | see, rename, purge, export definitions |
| `Explode` | break an instance back to geometry |

**When a block is worth it**: genuinely repeated elements — a mullion, a
balustrade, a tree. File size drops, and one edit fixes every copy.

**When it is ceremony**: things that are all slightly different. A facade of 340
unique panels is not a block problem; that is Week 11's problem.

> Blocks nest. That is powerful and it is how a file becomes impossible to
> reason about. Keep the nesting shallow.

## 6. Referencing other files

- **`Insert` as *linked***: the geometry lives in another file and updates when
  that file changes. Right for the site model everyone shares.
- **Worksessions** (`Worksession`): attach whole files alongside yours, visible
  and snappable but not editable. Right for a big shared context.

Either way the rule is the same: **do not copy the site into your file.** One
copy, referenced by everyone, updated once.

## 7. Model hygiene

Run these periodically, not just before a hand-in:

| | |
| --- | --- |
| `SelBadObjects` | invalid geometry, before it spreads |
| `ShowEdges` ▸ Naked | unjoined edges |
| `SelDup` | duplicates |
| `Purge` | unused layers, blocks, materials |
| `Audit3dmFile` | deeper report, for files from elsewhere |
| `ShrinkTrimmedSrf` | trimmed surfaces carrying huge hidden patches |

Full sequence, with what each is for:
[SELF-CHECK.md](/SELF-CHECK.md).

## 8. What to model and what to fake

The real decision of the week, and it is a judgement, not a rule.

**Model** what something downstream depends on — anything that gets dimensioned,
sectioned, panelised, costed or cut.

**Fake** what only ever appears in an image at 1:200.

The failure is not faking. It is faking **by accident**, and then forgetting
which is which. Put faked geometry on its own layer and it stays honest.

---

## Commands

The commands this week centres on. If one of these is not covered by the prose above, that's a signal to teach it — the list here is the week's source of truth for what students walk in expecting to use.

```
Move
Copy
Rotate
Rotate3D
Scale
Scale1D
Scale2D
Mirror
Align
Distribute
SetPt
Orient
Orient3Pt
OrientOnSrf
OrientOnCrv
ArrayLinear
ArrayPolar
ArrayCrv
ArraySrf
DupEdge
DupBorder
DupFaceBorder
ExtractSrf
ExtractIsocurve
ExtractControlPolygon
Silhouette
Intersect
Contour
ReplaceFace
ReplaceEdge
FilletEdge
ChamferEdge
OffsetSrf
ExtendSrf
RebuildEdges
RemoveEdge
MergeAllFaces
MergeSrf
Untrim
ShrinkTrimmedSrf
SelLayer
SelName
SelDup
SelClosedCrv
SelOpenCrv
SelectionFilter
SetObjectName
Block
Insert
BlockEdit
BlockManager
Worksession
Purge
Audit3dmFile
```
## Reference

- [Selection, Snapping & Precision](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/selection-snapping-precision) — §1
- [Transforms & Arrays](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/transforms-arrays) — §2
- [Surface & Solid Tools](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/surface-solid-tools) — §3 (`ExtractSrf`, `MergeAllFaces`, `OffsetSrf` …)
- [Curve Tools](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/curve-tools) — §3 (`DupEdge`, `DupBorder`, `Silhouette`, `Contour`)
- [Layers & Organization](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/layers-organization) — §4, §5, §7
- [Best Practices](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/best-practices) — §7, §8

---

Previous: [Week 02](/Lecture/Week_02/README.md) · Next: [Week 04](/Lecture/Week_04/README.md)
