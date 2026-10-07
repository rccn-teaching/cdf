# Week 09 — Curves and surfaces, parametrically

🧱 **Class build** · part 2 of 5

The class facade becomes a surface: UV, frames, and louvres that follow it.

## What this session covers

- the `t` parameter, and reparameterising to 0–1
- surface UV: the Week 01 rectangle again
- frames and planes: orient without fighting
- trims are masks, and surface components see the untrimmed rectangle

## In the room

**Today's goal:** The strip as a surface; a frame at each louvre position; a blade on each frame, aligned to the surface.

We build it together, live, from the data flow in [`goals.md`](/Lecture/Week_09/goals.md). At **3 critical points** I stop and you vote on what we place next (🗳️ in `goals.md`, polls run on `TBC-POLL-TOOL`), then we argue about the result before anyone touches the canvas. See [how the builds work](/README.md#how-the-builds-work).

You will not be given a `.gh` file. [Reading one teaches nothing, and the building is the skill](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition).

## Homework

- Put the louvre system on your own strip's surface, including its openings
- 🎓 iteration 1 is in two weeks: make it run end to end, roughly

## Commands

The commands this week centres on. If one of these is not covered by the prose above, that's a signal to teach it — the list here is the week's source of truth for what students walk in expecting to use.

```
Reparameterize
Divide Surface
Evaluate Surface
Surface Closest Point
Point In Trim
Evaluate Curve
Perp Frame
Orient
Rotate 3D
```
## Reference

Read before class; we will not spend session time on it.

- [rccn wiki → grasshopper/curve-operations](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/curve-operations)
- [rccn wiki → grasshopper/surface-mesh-operations](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/surface-mesh-operations)
- [rccn wiki → grasshopper/describing-a-definition](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition)

---

Previous: [Week 08](/Lecture/Week_08/README.md) · Next: [Week 10](/Lecture/Week_10/README.md)
