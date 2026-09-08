# Self-check

Run this on your own file before you hand anything in, and before you ask
anybody why something is not working. It takes about two minutes.

Every one of these is a Rhino command. There is no script, nothing to install,
and nothing that will not still be true in ten years.

## The two-minute pass

| | Command | You want |
| - | --- | --- |
| 1 | `Units` | metres or millimetres, absolute tolerance **0.001** |
| 2 | `SelBadObjects` | **nothing selected** |
| 3 | `ShowEdges` ▸ *Naked edges* | nothing lit up, except where an opening is intended |
| 4 | `SelDup` | nothing selected — duplicates hide inside each other |
| 5 | `Layer` | nothing on **Default**, every layer named `NN_NAME` |
| 6 | `SelLast` then `What` | the object type is what you think it is |
| 7 | `Zoom Extents` in every viewport | nothing stranded a kilometre from the origin |
| 8 | `Purge` | unused layers, blocks and materials gone |

If 1–4 are clean, most of what goes wrong later cannot happen.

## What each one is actually for

**`Units`** — tolerance is how close two things must be before Rhino agrees they
touch. Too loose and it joins things that are not aligned; too tight and nothing
joins at all. Roughly **1/1000 of the smallest thing you care about**. Set it
before you model, from the template — changing it later does not repair
geometry already built.

**`SelBadObjects`** — a bad object looks completely normal and will fail to
boolean, mesh, or export, with no useful message. Run this on any file you did
not make before you build on it. `Check` on a single object tells you *why* it
is bad.

**`ShowEdges`** — a naked edge is an edge not joined to anything. It is the
usual reason a boolean fails silently. If two surfaces should be joined and are
not, they are further apart than your tolerance.

**`SelDup`** — two identical objects on top of each other look like one. They
break booleans, double your panel schedule, and are invisible until they matter.

**`What`** — object type, valid or not, closed or not, degree, control point
counts, `u`/`v` domains, layer. Most "why is this behaving strangely" questions
are answered here in four seconds, and almost nobody opens it.

## Before a hand-in, also

- **`Purge`**, then `SaveAs` — file size should drop, sometimes a lot
- **`ShrinkTrimmedSrf`** on anything heavily trimmed — a 1 mm visible sliver can
  still carry a 50 m underlying patch
- Open it on **another machine**. A file that only works on yours is not done
- Look at it in **`Shaded`** and in **`Wireframe`**. Different things are wrong
  in each

## When a boolean fails

In this order, because it is nearly always one of these:

1. `SelBadObjects` — is either input invalid?
2. `ShowEdges` — is either input actually open?
3. `Units` — is tolerance sane for the size of what you are modelling?
4. Are the surfaces exactly coincident? Move one by a hair and retry
5. Only then look for a different way to model it

The workaround most people reach for — `Explode`, `Trim`, `Join` by hand —
produces something that looks right and is not closed. It will fail again later,
further from the cause.

## Why this is not automated

Because these are the commands you will use for the rest of your working life,
and a script that hid them behind a green tick would teach you to trust the tick
instead of the model.

The full reasoning behind each check:
[rccn wiki → NURBS Anatomy](https://kb.rccn.dev/computation/rhino-grasshopper/rhino/nurbs-anatomy).
