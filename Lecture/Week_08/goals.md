# Week 08 — goals

*Data trees II*

> A goal is a **data flow**, not a list of components. It says what has to
> happen, not how. Two people building the same goal will produce different
> definitions, and comparing them is the point.

You will not be given a `.gh` file for these. [Reading one teaches nothing and the building is the skill](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition).

---

## Goal 1 — Panelise a surface

**Together.** I build, you build, at the same time.

```mermaid
flowchart LR
    S["a surface"] --> G["UV grid"]
    G --> Q["a quad panel per cell"]
    Q --> V["what does the tree<br/>look like?"]
```

*Quads across a surface, and the panels arrive in some structure. Find out which.*

---

## Goal 2 — Keep the identity

**In pairs.** One drives, one navigates. Swap halfway.

```mermaid
flowchart LR
    Q["panels, grouped by row"] --> O["an operation on each"]
    O --> K["still grouped by row?"]
    K --> L["a label per panel:<br/>row, column"]
```

*Each panel should still know which row and column it is, after every operation.*

---

## Goal 3 — Fix it without flattening

**Alone.** From the diagram only. ~15 minutes, then compare.

```mermaid
flowchart LR
    Q["panels, wrong structure"] --> D["diagnose:<br/>where did the paths change?"]
    D --> F["fix it upstream"]
    F --> C["correct at the tree level,<br/>not just visually"]
```

*Flatten will make the picture right. Do it the other way and find out what flatten was hiding.*

---

## When you are done

Three definitions that satisfy three flows. None of them is *the* answer —
compare with the person next to you and find out where you disagreed.

If you finish early: break one. Change an input until it fails, and say
which part of the flow could not cope.
