# Week 05 — goals

*The canvas and the flow*

> A goal is a **data flow**, not a list of components. It says what has to
> happen, not how. Two people building the same goal will produce different
> definitions, and comparing them is the point.

You will not be given a `.gh` file for these. [Reading one teaches nothing and the building is the skill](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition).

---

## Goal 1 — Louvres along a line

**Together.** I build, you build, at the same time.

```mermaid
flowchart LR
    L["a line"] --> D["divide into n points"]
    D --> P["a plane at each point"]
    P --> B["a louvre blade on each plane"]
```

*Everything downstream is this shape: take something, divide it, put something at each division.*

---

## Goal 2 — Louvres that turn

**In pairs.** One drives, one navigates. Swap halfway.

```mermaid
flowchart LR
    L["a line"] --> D["divide into n points"]
    D --> P["a plane at each point"]
    A["angle slider"] --> R["rotate each plane"]
    P --> R
    R --> B["a blade on each plane"]
```

*One slider, one visible consequence. This is the moment a definition stops being a drawing.*

---

## Goal 3 — The same thing, on a curve

**Alone.** From the diagram only. ~15 minutes, then compare.

```mermaid
flowchart LR
    C["a curve"] --> D["divide into n points"]
    D --> P["a plane at each point,<br/>aligned to the curve"]
    P --> B["a blade on each plane"]
```

*If your definition only works on a straight line, you built a drawing with sliders attached.*

---

## When you are done

Three definitions that satisfy three flows. None of them is *the* answer —
compare with the person next to you and find out where you disagreed.

If you finish early: break one. Change an input until it fails, and say
which part of the flow could not cope.
