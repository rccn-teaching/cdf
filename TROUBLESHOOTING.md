# Troubleshooting

Run [SELF-CHECK.md](SELF-CHECK.md) first. It catches most of this in two minutes.

## Modelling

**A boolean failed and gave no reason.** Almost always one of: an invalid object
(`SelBadObjects`), an open polysurface (`ShowEdges` ▸ *Naked edges*), tolerance
wrong for the size you are modelling (`Units`), or two surfaces exactly
coincident. Check in that order.

**Two surfaces will not join.** Their edges are further apart than your absolute
tolerance. Either they genuinely do not meet, or your tolerance is too tight.
`ShowEdges` shows you where.

**`Cap` does nothing.** Cap only closes **planar** openings. If the opening is
not flat, you need a surface built another way — `Patch`, `NetworkSrf`, or
rebuilding the edge curves so they are planar.

**Fillet fails on an edge that looks fine.** Usually the radius is larger than
an adjacent face can absorb, or the edge meets others at a corner that cannot be
resolved. Try a smaller radius first to confirm which.

**`Trim` leaves the piece I wanted to remove.** You clicked the wrong side. Trim
removes what you pick. `Undo`, pick the other part.

**`UnrollSrf` refuses.** The surface is not developable — doubly-curved surfaces
cannot be flattened without distortion. That is geometry, not a bug. Approximate
with planar strips, triangulate, or accept the distortion and document it.

**Control points are miles away from the surface.** It is trimmed. They belong
to the underlying rectangular patch, not to what you can see —
[NURBS Anatomy](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/nurbs-anatomy).
`ShrinkTrimmedSrf` brings them closer.

**Something works on one box and not the identical one next to it.** Run `What`
on both. One is probably an **extrusion** and the other a polysurface.
`ConvertExtrusion` makes them the same.

**The file is enormous.** `Purge`, then `SaveAs`. Then `ShrinkTrimmedSrf` on
anything heavily trimmed. Then check for meshes you imported and forgot.

## Display and views

**I cannot see my geometry.** `Zoom Extents All`. If it flies off somewhere, you
have an object stranded far from the origin — `SelAll`, `Zoom Selected`, find it.

**Everything is faceted / low-poly.** That is the render mesh, not your geometry.
Adjust it in *Document Properties ▸ Mesh*, or `Options` ▸ *Mesh* — set it finer
before exporting or rendering.

**The gumball is pointing the wrong way.** It follows the active CPlane by
default. Either set the CPlane you want, or switch the gumball to *World* or
*Object* alignment.

**My layout print is the wrong scale.** Detail scale is set per detail, not for
the layout. Double-click into the detail, then `Properties` ▸ set the scale, then
**lock the detail** so it cannot be nudged.

## Grasshopper

**It works for me and not for my classmate.** You referenced Rhino geometry
instead of internalising it. Right-click the parameter ▸ *Internalise data*.

**A component is orange.** A warning — it ran, but something is off. Hover for
the message. Orange usually means empty or partially-empty input.

**A component is red.** An error — it did not run. Hover for the message, and
look upstream: the real cause is often two or three components earlier.

**I get far more items than I expected.** A data tree problem, and almost always
a cross-reference or a graft where you wanted matching lists. Attach a Param
Viewer and read the structure before changing anything.

**Grasshopper is slow.** Turn off preview on components you are not looking at,
and check whether a tree has quietly become enormous. The Param Viewer tells you
how many items you are actually making.

**An AI assistant described a component that does not exist.** It does that —
assistants are markedly weaker on Grasshopper than on text. Treat anything one
says about components as a hypothesis to test on the canvas.

## Rhino itself

**Rhino will not start / licence error.** The class licence server needs you on
the campus network or VPN. See [SETUP.md](SETUP.md), then ask.

**Rhino crashed and I lost work.** Check the autosave location in *Options ▸
Files*. Then start saving incrementally — `IncrementalSave` gives you
`name_01.3dm`, `name_02.3dm`, and costs nothing.

## Still stuck

Ask your pod first — four other people are hitting the same things. If it
survives that, bring: what you were trying to do, what you tried, and the file.
