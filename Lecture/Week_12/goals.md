# Week 12 — goals

*Meshes*

> A goal is a **data flow**, not a list of components. It says what has to
> happen, not how. Two people building the same goal will produce different
> definitions, and comparing them is the point.

You will not be given a `.gh` file for these. [Reading one teaches nothing and the building is the skill](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition).

---

## Goal 1 — Mesh from a surface

**Together.** I build, you build, at the same time.

```mermaid
flowchart LR
    S["a surface"] --> M["mesh it"]
    M --> N["find naked edges"]
    N --> Q["is the topology<br/>what you expected?"]
```

*Convert, then look at what you got. Naked edges tell you whether it is sound.*

---

## Goal 2 — Weld and smooth

**In pairs.** One drives, one navigates. Swap halfway.

```mermaid
flowchart LR
    M["a mesh"] --> W["weld the vertices"]
    W --> S["smooth it"]
    S --> C["compare vertex counts<br/>before and after"]
```

*Duplicate vertices look identical and break everything downstream.*

---

## Goal 3 — Something NURBS would fight you on

**Alone.** From the diagram only. ~15 minutes, then compare.

```mermaid
flowchart LR
    I["a rough input:<br/>scan, terrain, or blob"] --> M["mesh operations"]
    M --> R["a usable surface"]
    R --> J["why would this have been<br/>miserable in NURBS?"]
```

*Pick a form where the mesh is obviously the right tool, and say why.*

---

## When you are done

Three definitions that satisfy three flows. None of them is *the* answer —
compare with the person next to you and find out where you disagreed.

If you finish early: break one. Change an input until it fails, and say
which part of the flow could not cope.
