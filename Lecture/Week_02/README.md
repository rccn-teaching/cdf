# Week 02 — Making things: curves into surfaces

> **This page is the reference.** The session is a demo; this is the map.

Last week was what things *are*. This week is how you make them, and the whole
week rests on one sentence: **a surface is only as good as the curves
underneath it.**

---

## 1. Curves worth knowing

| Command | For |
| --- | --- |
| `Line` `Polyline` `Arc` `Circle` `Rectangle` | the obvious ones |
| `InterpCrv` | a curve **through** points you pick |
| `Curve` | a curve **controlled by** points you pick |
| `BlendCrv` | a curve joining two others, with controllable continuity |
| `Offset` | parallel copy |
| `Fillet` `Chamfer` | round or cut a corner |
| `CurveBoolean` | **regions from overlapping curves** — see below |
| `Project` `Pull` | get a curve onto a surface |

**`InterpCrv` vs `Curve`** catches everyone: the first passes *through* your
points, the second is *pulled toward* them. Same clicks, different result.

**`Project` vs `Pull`**: `Project` drops the curve along the CPlane normal;
`Pull` moves each point to the closest point on the surface. On a steep surface
these differ a lot.

### `CurveBoolean` — the command most people never find

Pick regions bounded by overlapping curves and get clean closed results. Far
faster than trimming by hand, and far less likely to leave a gap you do not
notice until the laser cutter does.

### Continuity: G0, G1, G2

- **G0** — they touch
- **G1** — they touch and are **tangent**
- **G2** — they touch, are tangent, and have **matching curvature**

G2 is what reads as "designed" and reflects light without a visible crease.

**You cannot see the difference by eye on a screen.** Use the tools:

| | Shows |
| --- | --- |
| `Zebra` | stripes; a break at a seam means less than G2 |
| `EMap` | environment reflection, same idea |
| `CurvatureGraph` | the actual curvature, as a graph off the curve |

## 2. Surfaces from curves

| Command | Use when |
| --- | --- |
| `ExtrudeCrv` | straight extrusion |
| `Loft` | you have section curves, in order |
| `Sweep1` | one rail, one or more sections |
| `Sweep2` | two rails — more control, more ways to fail |
| `Revolve` | rotationally symmetric |
| `NetworkSrf` | a grid of curves both ways. Forgiving, and heavier |
| `Patch` | fill a hole with something roughly right |

**Clean input, clean output.** Curves with mismatched control point counts make
lumpy surfaces. `Rebuild` them to match *before* lofting, not after.

**`Cap`** closes **planar** openings — that is how most solids get made. If
`Cap` does nothing, the opening is not flat: use `Patch`, or rebuild the edge
curves so they are planar.

## 3. Editing what you made

| Command | Does |
| --- | --- |
| `Trim` | removes the part you **click** |
| `Split` | keeps **both** parts as separate objects |
| `Join` | welds within tolerance (Week 01 §6) |
| `Explode` | polysurface back into faces |
| `FilletEdge` `ChamferEdge` | round or cut a solid's edges |
| `OffsetSrf` | thicken a surface into a solid |
| `BooleanUnion` `BooleanDifference` `BooleanIntersection` | combine solids |

**`FilletEdge` fails** when the radius is larger than an adjacent face can
absorb, or where several edges meet at one corner. Try a smaller radius to find
out which it is.

**Trimming with a curve that only *looks* like it crosses the surface** —
because you are seeing it from one viewport — is a classic wasted afternoon.
Check in a second view first.

## 4. Placing things exactly

| | |
| --- | --- |
| `Move` `Copy` `Rotate` `Scale` `Mirror` | the basics |
| `Align` | edges or centres, in one axis |
| `Distribute` | even spacing across a set |
| **`SetPt`** | set X, Y and/or Z of many objects to one value |
| `Orient` `Orient3Pt` | move by picking references, not typing numbers |
| `ArrayLinear` `ArrayPolar` `ArrayCrv` | repeat along a line, circle, or curve |

**`SetPt`** is the underused one: flattening a scattered set of points to a
single Z is two clicks.

### Snapping

**Osnaps** — End, Mid, Cen, Int, Perp, Tan, Quad, Near — are persistent, in the
bar at the bottom. Turn on only the ones you need; all of them at once fight
each other.

> **`Project` in the osnap bar** forces every snapped point onto the CPlane.
> That is either exactly what you want, or the reason everything landed at
> `z = 0`. Know which state it is in.

**`Ortho`** (hold <kbd>Shift</kbd>), **grid snap** (<kbd>F9</kbd>), and
`SmartTrack` for construction lines are worth ten minutes of play.

**The gumball** is fast, and it follows the active **CPlane** — the Week 01
callback.

---

## Commands

The commands this week centres on. If one of these is not covered by the prose above, that's a signal to teach it — the list here is the week's source of truth for what students walk in expecting to use.

```
BlendCrv
CurveBoolean
Fillet
Project
Pull
Loft
Sweep1
Sweep2
NetworkSrf
Cap
Trim
Split
FilletEdge
OffsetSrf
Zebra
EMap
CurvatureGraph
```
## Reference

- [Curve Tools](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/curve-tools)
- [Surface & Solid Tools](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/surface-solid-tools)
- [Transforms & Arrays](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/transforms-arrays)
- [Selection, Snapping & Precision](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/selection-snapping-precision)

---

Previous: [Week 01](/Lecture/Week_01/README.md) · Next: [Week 03](/Lecture/Week_03/README.md)
