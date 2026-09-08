# Week 07 — goals

*Data trees I*

> A goal is a **data flow**, not a list of components. It says what has to
> happen, not how. Two people building the same goal will produce different
> definitions, and comparing them is the point.

You will not be given a `.gh` file for these. [Reading one teaches nothing and the building is the skill](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition).

---

## Goal 1 — A grid of points, flat

**Together.** I build, you build, at the same time.

```mermaid
flowchart LR
    S["a surface"] --> U["divide U into nu"]
    S --> V["divide V into nv"]
    U --> P["all points, one flat list"]
    V --> P
```

*Build it the naive way first, so you can feel what is missing.*

---

## Goal 2 — The same grid, as a tree

**In pairs.** One drives, one navigates. Swap halfway.

```mermaid
flowchart LR
    S["a surface"] --> G["divide into a UV grid"]
    G --> T["points, grouped:<br/>one branch per row"]
    T --> V["read the paths<br/>in the Param Viewer"]
```

*One branch per row. Same points, entirely different behaviour downstream.*

---

## Goal 3 — A circle at each point, sized by row

**Alone.** From the diagram only. ~15 minutes, then compare.

```mermaid
flowchart LR
    T["points, one branch per row"] --> N["a radius per row"]
    N --> C["a circle at each point"]
    T --> C
```

*The payoff: because the data is grouped by row, a per-row value just works.*

---

## When you are done

Three definitions that satisfy three flows. None of them is *the* answer —
compare with the person next to you and find out where you disagreed.

If you finish early: break one. Change an input until it fails, and say
which part of the flow could not cope.
