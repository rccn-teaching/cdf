# Week 14 — goals

*Fabrication prep*

> A goal is a **data flow**, not a list of components. It says what has to
> happen, not how. Two people building the same goal will produce different
> definitions, and comparing them is the point.

You will not be given a `.gh` file for these. [Reading one teaches nothing and the building is the skill](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition).

---

## Goal 1 — Unroll one panel

**Together.** I build, you build, at the same time.

```mermaid
flowchart LR
    P["one panel"] --> U["unroll to the XY plane"]
    U --> C["compare edge lengths<br/>with the original"]
```

*One. Get it flat and correct before you try three hundred.*

---

## Goal 2 — Label every panel

**In pairs.** One drives, one navigates. Swap halfway.

```mermaid
flowchart LR
    P["all panels"] --> I["an id per panel:<br/>row, column"]
    I --> U["unroll each"]
    U --> T["the id, as text,<br/>on the flat panel"]
```

*Identity has to survive from the surface all the way to the cut file.*

---

## Goal 3 — Nest and schedule

**Alone.** From the diagram only. ~15 minutes, then compare.

```mermaid
flowchart LR
    F["flat labelled panels"] --> N["nest on a sheet"]
    N --> S["count sheets,<br/>compute waste"]
    S --> Q["a schedule you can<br/>hand to a fabricator"]
```

*The number at the bottom has to be true, and you have to be able to say why.*

---

## When you are done

Three definitions that satisfy three flows. None of them is *the* answer —
compare with the person next to you and find out where you disagreed.

If you finish early: break one. Change an input until it fails, and say
which part of the flow could not cope.
