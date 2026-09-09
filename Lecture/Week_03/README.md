# Week 03 — Working at scale

> **This page is the reference.** Unglamorous, and the week that decides whether
> Week 14 is possible.

A model you cannot navigate is a model you cannot finish. Everything here is
about finding, selecting and reusing — the things that stop mattering at ten
objects and decide everything at ten thousand.

---

## 1. Selecting what you mean

Clicking is the slow way. The `Sel*` family is the fast way.

| Command | Selects |
| --- | --- |
| `SelLayer` | everything on a layer |
| `SelName` | everything with a given object name |
| **`SelDup`** | duplicates sitting exactly on top of each other |
| `SelBadObjects` | invalid geometry |
| `SelCrv` `SelSrf` `SelPolysrf` `SelMesh` | by type |
| `SelClosedCrv` `SelOpenCrv` | by state |
| `SelLast` `SelPrev` | what you just made, or just had selected |
| `Invert` | everything else |
| `SelAll` `SelNone` | |

**`SelDup` is the one to run periodically.** Two identical objects look like
one, break booleans, double a panel schedule, and stay invisible until they cost
you.

### Window vs crossing

- **Left → right**: takes only what is **fully inside** the box
- **Right → left**: takes anything the box **touches**

Most people use one of these their whole life without noticing the other exists.

**`SelectionFilter`** restricts what is selectable at all — invaluable when
picking curves out of a dense model.

## 2. Naming, and why it pays later

`Properties` ▸ Name, or `SetObjectName`. A named object can be found with
`SelName`, and — the part that matters — **referenced by name from Grasshopper**
from Week 05 onward.

Name the things a definition will need to grab. Not everything.

## 3. Blocks

A **block** is one definition placed many times. Edit the definition, every
instance updates.

| Command | Does |
| --- | --- |
| `Block` | make a definition from selected geometry |
| `Insert` | place an instance |
| `BlockEdit` | edit the definition in place |
| `BlockManager` | see, rename, purge, export definitions |
| `Explode` | break an instance back to geometry |

**When a block is worth it**: genuinely repeated elements — a mullion, a
balustrade, a tree. File size drops, and one edit fixes every copy.

**When it is ceremony**: things that are all slightly different. A facade of 340
unique panels is not a block problem; that is Week 11's problem.

> Blocks nest. That is powerful and it is how a file becomes impossible to
> reason about. Keep the nesting shallow.

## 4. Referencing other files

- **`Insert` as *linked***: the geometry lives in another file and updates when
  that file changes. Right for the site model everyone shares.
- **Worksessions** (`Worksession`): attach whole files alongside yours, visible
  and snappable but not editable. Right for a big shared context.

Either way the rule is the same: **do not copy the site into your file.** One
copy, referenced by everyone, updated once.

## 5. Model hygiene

Run these periodically, not just before a hand-in:

| | |
| --- | --- |
| `SelBadObjects` | invalid geometry, before it spreads |
| `ShowEdges` ▸ Naked | unjoined edges |
| `SelDup` | duplicates |
| `Purge` | unused layers, blocks, materials |
| `Audit3dmFile` | deeper report, for files from elsewhere |
| `ShrinkTrimmedSrf` | trimmed surfaces carrying huge hidden patches |

Full sequence, with what each is for:
[SELF-CHECK.md](/SELF-CHECK.md).

## 6. What to model and what to fake

The real decision of the week, and it is a judgement, not a rule.

**Model** what something downstream depends on — anything that gets dimensioned,
sectioned, panelised, costed or cut.

**Fake** what only ever appears in an image at 1:200.

The failure is not faking. It is faking **by accident**, and then forgetting
which is which. Put faked geometry on its own layer and it stays honest.

---

## Commands

The commands this week centres on. If one of these is not covered by the prose above, that's a signal to teach it — the list here is the week's source of truth for what students walk in expecting to use.

```
SelLayer
SelName
SelDup
SelClosedCrv
SelOpenCrv
SelectionFilter
SetObjectName
Block
Insert
BlockEdit
BlockManager
Worksession
Purge
Audit3dmFile
```
## Reference

- [Layers & Organization](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/layers-organization)
- [Selection, Snapping & Precision](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/selection-snapping-precision)
- [Best Practices](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/best-practices)
- [Transforms & Arrays](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/transforms-arrays)

---

Previous: [Week 02](/Lecture/Week_02/README.md) · Next: [Week 04](/Lecture/Week_04/README.md)
