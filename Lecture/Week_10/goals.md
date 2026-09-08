# Week 10 — goals

*Attractors, remapping, fields*

> A goal is a **data flow**, not a list of components. It says what has to
> happen, not how. Two people building the same goal will produce different
> definitions, and comparing them is the point.

You will not be given a `.gh` file for these. [Reading one teaches nothing and the building is the skill](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition).

---

## Goal 1 — Radius by distance

**Together.** I build, you build, at the same time.

```mermaid
flowchart LR
    P["points on a grid"] --> A["distance to an attractor"]
    A --> R["use it as a radius"]
    R --> C["a circle at each point"]
```

*The raw response. It will look wrong, and the reason it looks wrong is the next goal.*

---

## Goal 2 — Remap into a range you chose

**In pairs.** One drives, one navigates. Swap halfway.

```mermaid
flowchart LR
    A["distances"] --> M["measure the actual range"]
    M --> R["remap to 0.2 – 1.0"]
    R --> C["a circle at each point"]
```

*Name both domains out loud. Most remap bugs are guessing the source instead of measuring it.*

---

## Goal 3 — A falloff you can defend

**Alone.** From the diagram only. ~15 minutes, then compare.

```mermaid
flowchart LR
    A["distances"] --> R["remap to 0 – 1"]
    R --> G["shape the falloff curve"]
    G --> S["scale to real dimensions"]
    S --> O["an aperture at each point"]
```

*Shape the response deliberately, and be ready to say what the driver is.*

---

## When you are done

Three definitions that satisfy three flows. None of them is *the* answer —
compare with the person next to you and find out where you disagreed.

If you finish early: break one. Change an input until it fails, and say
which part of the flow could not cope.
