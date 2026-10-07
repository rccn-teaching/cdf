# Week 12 — A site from survey points: meshes

🔹 **Standalone build**

When NURBS is the wrong tool: a terrain mesh from a surveyor's points, its slopes, and its contours.

## What this session covers

- mesh vs NURBS: what each is good at, what each costs
- topology: vertices, faces, naked edges, welding
- when to convert, and in which direction
- meshes from scans and surveys

## In the room

**Today's goal:** The site terrain from a cloud of survey points: a mesh, its slope shown as colour, contours every 0.5 m for the site model.

We build it together, live, from the data flow in [`goals.md`](/Lecture/Week_12/goals.md). At **3 critical points** I stop and you vote on what we place next (🗳️ in `goals.md`, polls run on `TBC-POLL-TOOL`), then we argue about the result before anyone touches the canvas. See [how the builds work](/README.md#how-the-builds-work).

You will not be given a `.gh` file. [Reading one teaches nothing, and the building is the skill](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition).

## Homework

- Decide **in writing** whether your system is NURBS or mesh, and what would make you switch

## Commands

The commands this week centres on. If one of these is not covered by the prose above, that's a signal to teach it — the list here is the week's source of truth for what students walk in expecting to use.

```
Delaunay Mesh
Mesh Surface
Mesh Brep
Face Normals
Angle
Mesh Edges
Weld Mesh
Contour
Custom Preview
Gradient
```
## Reference

Read before class; we will not spend session time on it.

- [rccn wiki → grasshopper/surface-mesh-operations](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/surface-mesh-operations)
- [rccn wiki → workflows/mesh-relaxation](https://kb.rccn.dev/computation/rhino-grasshopper/workflows/mesh-relaxation)
- [rccn wiki → grasshopper/describing-a-definition](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition)

---

Previous: [Week 11](/Lecture/Week_11/README.md) · Next: [Week 13](/Lecture/Week_13/README.md)
