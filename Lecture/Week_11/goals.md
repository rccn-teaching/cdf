# Week 11 — goals

*Panelisation and subdivision*

> A goal is a **data flow**, not a list of components. It says what has to
> happen, not how. Two people building the same goal will produce different
> definitions, and comparing them is the point.

You will not be given a `.gh` file for these. [Reading one teaches nothing and the building is the skill](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition).

---

## Goal 1 — Quads on a surface

**Together.** I build, you build, at the same time.

```mermaid
flowchart LR
    S["a surface"] --> G["UV grid"]
    G --> Q["a quad panel per cell"]
```

*The straightforward case, so the failure in goal 3 is legible.*

---

## Goal 2 — An aperture per panel

**In pairs.** One drives, one navigates. Swap halfway.

```mermaid
flowchart LR
    Q["quad panels"] --> F["a frame per panel"]
    F --> A["an aperture,<br/>sized per panel"]
    A --> P["panel with opening"]
```

*Each panel needs its own frame, and the aperture has to sit in it.*

---

## Goal 3 — Make them planar

**Alone.** From the diagram only. ~15 minutes, then compare.

```mermaid
flowchart LR
    Q["quad panels"] --> M["measure planarity"]
    M --> D{{"acceptable?"}}
    D -->|no| T["triangulate<br/>or approximate"]
    D -->|yes| K["keep, and document<br/>the tolerance"]
```

*A quad on a double-curved surface is not flat. Triangulate, approximate, or measure the warp and argue for it.*

---

## When you are done

Three definitions that satisfy three flows. None of them is *the* answer —
compare with the person next to you and find out where you disagreed.

If you finish early: break one. Change an input until it fails, and say
which part of the flow could not cope.
