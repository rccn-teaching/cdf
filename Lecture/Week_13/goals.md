# Week 13 — goals

*Form-finding*

> A goal is a **data flow**, not a list of components. It says what has to
> happen, not how. Two people building the same goal will produce different
> definitions, and comparing them is the point.

You will not be given a `.gh` file for these. [Reading one teaches nothing and the building is the skill](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition).

---

## Goal 1 — Relax a flat mesh

**Together.** I build, you build, at the same time.

```mermaid
flowchart LR
    M["a flat mesh"] --> A["anchor some vertices"]
    A --> S["solver"]
    S --> R["a relaxed mesh"]
```

*Anchors and nothing else. Watch it do very little, and understand why.*

---

## Goal 2 — Add springs with a rest length

**In pairs.** One drives, one navigates. Swap halfway.

```mermaid
flowchart LR
    M["a mesh"] --> E["springs on the edges,<br/>with a rest length"]
    M --> A["anchors"]
    E --> S["solver"]
    A --> S
    S --> R["a found form"]
```

*Now the constraints fight each other, which is where form comes from.*

---

## Goal 3 — Relax onto a constraint you choose

**Alone.** From the diagram only. ~15 minutes, then compare.

```mermaid
flowchart LR
    M["a mesh"] --> C["a constraint that means<br/>something physically"]
    C --> S["solver"]
    S --> R["a form"]
    R --> J["what does your<br/>constraint mean?"]
```

*The constraints are the design. The shape is a consequence.*

---

## When you are done

Three definitions that satisfy three flows. None of them is *the* answer —
compare with the person next to you and find out where you disagreed.

If you finish early: break one. Change an input until it fails, and say
which part of the flow could not cope.
