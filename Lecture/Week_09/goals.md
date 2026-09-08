# Week 09 — goals

*Curves and surfaces, parametrically*

> A goal is a **data flow**, not a list of components. It says what has to
> happen, not how. Two people building the same goal will produce different
> definitions, and comparing them is the point.

You will not be given a `.gh` file for these. [Reading one teaches nothing and the building is the skill](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition).

---

## Goal 1 — Circles along a curve

**Together.** I build, you build, at the same time.

```mermaid
flowchart LR
    C["a curve"] --> D["divide into n"]
    D --> P["a plane at each point,<br/>aligned to the curve"]
    P --> O["a circle on each plane"]
```

*Divide, evaluate, place. The `t` parameter is the whole idea.*

---

## Goal 2 — A component oriented to a surface

**In pairs.** One drives, one navigates. Swap halfway.

```mermaid
flowchart LR
    S["a surface"] --> G["UV grid"]
    G --> F["a frame at each node,<br/>normal to the surface"]
    F --> C["orient a component<br/>onto each frame"]
```

*The frames are the hard part. Getting them wrong looks almost right, which is worse.*

---

## Goal 3 — Along a curve, on a surface

**Alone.** From the diagram only. ~15 minutes, then compare.

```mermaid
flowchart LR
    S["a surface"] --> C["a curve on it"]
    C --> D["divide the curve"]
    D --> F["a frame at each point,<br/>using the surface normal"]
    F --> O["a component on each"]
```

*Two parameter spaces at once. If it twists, decide whether that is the frame or the surface.*

---

## When you are done

Three definitions that satisfy three flows. None of them is *the* answer —
compare with the person next to you and find out where you disagreed.

If you finish early: break one. Change an input until it fails, and say
which part of the flow could not cope.
