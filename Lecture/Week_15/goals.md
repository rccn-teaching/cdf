# Week 15 — goals

*Definition hygiene*

> A goal is a **data flow**, not a list of components. It says what has to
> happen, not how. Two people building the same goal will produce different
> definitions, and comparing them is the point.

You will not be given a `.gh` file for these. [Reading one teaches nothing and the building is the skill](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition).

---

## Goal 1 — Make it readable

**Together.** I build, you build, at the same time.

```mermaid
flowchart LR
    D["your definition"] --> G["group by purpose"]
    G --> N["name the groups"]
    N --> P["gather the driving<br/>parameters in one place"]
```

*Someone else has to find the parameter that matters. Time them.*

---

## Goal 2 — Make it portable

**In pairs.** One drives, one navigates. Swap halfway.

```mermaid
flowchart LR
    D["your definition"] --> I["internalise the inputs"]
    I --> T["open it on<br/>another machine"]
    T --> V["does it still run?"]
```

*A definition that only runs on your machine is not finished.*

---

## Goal 3 — Make it fast

**Alone.** From the diagram only. ~15 minutes, then compare.

```mermaid
flowchart LR
    D["your definition"] --> M["measure: which<br/>components are slow?"]
    M --> P["previews off<br/>where not needed"]
    M --> T["is a tree quietly<br/>enormous?"]
```

*Find what is actually slow rather than what you assume is slow.*

---

## When you are done

Three definitions that satisfy three flows. None of them is *the* answer —
compare with the person next to you and find out where you disagreed.

If you finish early: break one. Change an input until it fails, and say
which part of the flow could not cope.
