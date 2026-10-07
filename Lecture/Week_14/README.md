# Week 14 — Fabrication prep: flatten, label, lay out

🧱 **Class build** · part 4 of 5

The class facade leaves the computer: every panel laid flat, labelled with its W11 identity, nested on sheets, and counted.

## What this session covers

- laying planar panels flat; unrolling what is not planar
- nesting, sheet efficiency, and material constraints as inputs
- labelling: identity surviving to the cut file
- tolerance and kerf: the gap between model and machine

## In the room

**Today's goal:** Cut sheets for the strip's panels: flat, labelled, kerf-offset, laid out on 2440 × 1220 sheets, plus a panel schedule.

We build it together, live, from the data flow in [`goals.md`](/Lecture/Week_14/goals.md). At **3 critical points** I stop and you vote on what we place next (🗳️ in `goals.md`, polls run on `TBC-POLL-TOOL`), then we argue about the result before anyone touches the canvas. See [how the builds work](/README.md#how-the-builds-work).

You will not be given a `.gh` file. [Reading one teaches nothing, and the building is the skill](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition).

## Homework

- 🎓 **Iteration 2**: fabricable, scheduled, unrolled, on your strip

## Commands

The commands this week centres on. If one of these is not covered by the prose above, that's a signal to teach it — the list here is the week's source of truth for what students walk in expecting to use.

```
Orient
Unroll Brep
Offset Curve
Bounding Box
Text Tag 3D
OpenNest: Nest
Create Set
Member Index
Sort Along Curve
Bake
```
## Reference

Read before class; we will not spend session time on it.

- [rccn wiki → workflows/fabrication-prep](https://kb.rccn.dev/computation/rhino-grasshopper/workflows/fabrication-prep)
- [rccn wiki → grasshopper/interop-baking-attributes](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/interop-baking-attributes)
- [rccn wiki → grasshopper/describing-a-definition](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition)

---

Previous: [Week 13](/Lecture/Week_13/README.md) · Next: [Week 15](/Lecture/Week_15/README.md)
