# Week 05 — Grasshopper essentials

Onboarding and a cheatsheet: everything about *operating* Grasshopper, before
any of it is about *design*.

> **This page is the exception to the course's rule** that reference lives on
> the wiki. Like Week 01, it is written out in full, because from Week 06 every
> session is a live build. When we pause and ask "which component next?",
> nobody should be stuck on *how* to place it, wire it or see it. Keep this
> page open beside the canvas for the rest of the term.
>
> Data trees are **not** here. They get their own week, Week 08, once you have
> run into them.

---

## 1. Starting up

```
_Grasshopper
```

Type it in Rhino's command line. Grasshopper opens in its own window, and
**its preview appears in Rhino's viewports, but nothing in that preview is
Rhino geometry** until you *bake* it (§7). Hold onto that sentence; most
first-week confusion is about it.

| Part of the window | What it is |
| --- | --- |
| **ribbon tabs** | Params · Maths · Sets · Vector · Curve · Surface · Mesh · Intersect · Transform · Display · *Rhino* (Rhino 8). Each tab is divided into panels |
| **canvas** | where the definition lives; data flows **left → right** |
| **canvas toolbar** | open/save, zoom, and the **preview** buttons (§5) |
| **Solution menu** | recompute (`F5`), and disabling the solver while you edit something heavy |

A definition saves as `.gh` (binary) or `.ghx` (XML, larger, readable by a
text editor). It is **separate from your `.3dm`**: saving the Rhino file does
not save the definition, and the other way round. Save both, and keep them in
the same folder.

## 2. Two kinds of object on the canvas

| | **Params** | **Components** |
| --- | --- | --- |
| do | *hold* data | *do* something to data |
| look like | one box, one grip each side | inputs on the left, outputs on the right |
| examples | Number Slider, Panel, Point, Curve | Divide Curve, Move, Loft |
| use them to | see, store, reference, steer | transform |

**A component's colour is a message.** Grey: fine. **Orange**: a warning, it
ran but something is off (often an empty input). **Red**: an error, it did not
run. Hover the little balloon at the top for the message. Read it before
anything else.

**A wire's look tells you what flows through it.** A thin single line is one
item, a double line is a list, and a dashed line is a *tree* (Week 08). Wires
also run left to right; a wire that doubles back is a definition that is hard
to read.

## 3. Finding and placing components

| Do this | How |
| --- | --- |
| **Search** for a component | **double-click empty canvas**, type part of its name, `Enter` |
| place a **slider with a range** in one go | double-click, type `0<5<10` (min < value < max) |
| place a **slider** | double-click, type a number, e.g. `12` |
| find **where a component lives** in the ribbon | hold **`Ctrl` + `Alt`** and press on a component on the canvas |
| **find** a component already somewhere on a big canvas | `Ctrl` + `F` |
| read what a component does | hover it, or right-click ▸ *Help* |
| see components hidden from the ribbon | some components are **"obscure"**: kept out of the ribbon to save space. Search still finds them, and each ribbon panel's drop-down lists everything in it |
| radial menu (common actions under the cursor) | **middle-click** on the canvas |

> **Search by what it does, not what you think it is called.** "divide",
> "closest", "remap" find more than guessing a component's exact name. When
> two results look alike, place both and read their inputs; the inputs tell you
> what each one is for.

## 4. Wires

| Do this | How |
| --- | --- |
| connect | drag from an output grip to an input grip |
| **add** a second wire to an input | hold **`Shift`** while dragging |
| **remove** a wire | hold **`Ctrl`** and drag over the same connection |
| **move** all wires from one grip to another | hold **`Ctrl` + `Shift`** and drag from the grip |
| quieten a busy wire | right-click the **input** ▸ *Wire Display* ▸ **Default / Faint / Hidden** |
| add an input to a component that allows it | zoom in until `+` / `−` appear on its side |

A *hidden* wire still carries data. Use *Faint* on the long wires that cross
the whole canvas (a site, a main slider), and never hide a wire you are still
debugging.

## 5. Seeing what you are doing: preview and display

| Do this | How |
| --- | --- |
| switch one component's preview off / on | select it, **`Ctrl` + `Q`** (or right-click ▸ *Preview*) |
| **disable** a component (it stops computing; everything downstream goes empty) | select it, **`Ctrl` + `E`** |
| preview **only what is selected** | the canvas-toolbar button *"only draw preview geometry for selected objects"*. The single most useful button in a big definition |
| change preview to wireframe / shaded / none | canvas-toolbar preview buttons |
| colour a preview on purpose | **Custom Preview**, fed a colour or a Swatch |
| see the data, not the geometry | a **Panel** on the output (§6) |

**Preview off and disabled are different things.** Preview off: it still runs,
you just do not see it. Disabled: it does not run, and everything downstream
loses its data. Use preview off to declutter. Use disable to stop something
slow while you work elsewhere.

## 6. The panel: the only debugger you get

Wire any output into a **Panel** and you see exactly what is flowing: numbers,
text, how many items. Right-click the panel for:

- **Draw Indices**: the index of each item (0, 1, 2 …)
- **Draw Paths**: the tree branches, `{0;0}` and so on (Week 08)
- **Multiline Data**: wrap long values

Before you "fix" anything, put a panel on it and read what is really there.
Most Grasshopper problems are not wrong components but wrong *data*: an empty
list, one item where you expected ten, numbers in the wrong order.

## 7. Rhino ↔ Grasshopper: reference, internalise, bake

### Getting geometry *in*: referencing

Right-click a geometry param (Point, Curve, Brep …) ▸ **Set one …** or
**Set Multiple …**, then pick in Rhino. The param now *points at* that Rhino
object: move it in Rhino and the definition updates live.

The catch: the definition now depends on that exact object in that exact
`.3dm`. Open the `.gh` on another machine without the file and it is empty.
So, once the geometry is final:

**Right-click ▸ Internalise data.** The geometry is copied *into* the `.gh`
and the link to Rhino is cut. Internalise anything that has to travel with the
definition, which is everything you submit. (The project brief says the
definition must open elsewhere; this is how.)

### Getting geometry *out*: baking

Right-click a component with a geometry output ▸ **Bake …**, and choose the
layer. Now it is real Rhino geometry, but a **frozen copy**: change a slider
and the baked object does not follow. Bake late, and bake on purpose: to
draft it (Week 04's tools), to hand it to someone, or to fabricate it.

Rhino 8 adds components on the *Rhino* tab for reading and writing Rhino model
objects with their layer, name and colour from inside the definition. The wiki
covers them: [interop & baking](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/interop-baking-attributes).

## 8. Many ways to make a point, and when to use each

The simplest geometry has five common sources, and choosing between them is
your first real design decision in Grasshopper: **where should this value come
from?**

| Method | How | Use it when |
| --- | --- | --- |
| **Panel with text** | a Panel containing `3,4,0`, wired into a Point input; Grasshopper converts the text | the value is **fixed and known**, and you want it written down where a reader sees it |
| **Sliders + Construct Point** | three Number Sliders into *Construct Point* (x, y, z) | the value is a **parameter you will steer**. Name the sliders |
| **MD Slider** | one two-dimensional slider gives an x, y pair | quick 2D exploration by dragging; not precise, hard to read later |
| **Reference from Rhino** | Point param ▸ *Set one Point* | the location **belongs to the model**: a site corner, a column on the base building, something placed by eye. Internalise before submitting |
| **Computed** | the output of another component: *Divide Curve*, *Evaluate Curve*, *Curve Closest Point* … | the point is **a consequence** of other geometry. This is the Grasshopper way, and most points in a good definition are made like this |

A definition full of referenced and typed points is a drawing with extra
steps. A definition whose points are mostly *computed* from a few named inputs
is a system, and only a system is steerable.

## 9. Rhino or Grasshopper?

Grasshopper is not "better Rhino". It is a different tool, with a cost: every
decision has to be written as a rule. Choose per task:

| Use **Rhino** when | Use **Grasshopper** when |
| --- | --- |
| you will do it **once** | you will do it **many times**, or many **instances** of it |
| the form is found by **hand and eye** (SubD sculpting, a free curve) | the form follows a **rule** (spacing, a driver, a constraint) |
| you are **fixing**: cleaning, trimming, rebuilding a surface | you will **change your mind** about a number later |
| you are **drafting**: layouts, sections, annotation (Week 04) | you need **traceability**: where did this panel's size come from? |
| the rule would take longer to write than the result to draw | the result is too repetitive or too precise to draw |

The common workflow is both: model the *givens* in Rhino (site, base building,
a hand-drawn curve), reference them into Grasshopper, generate the *system*
there, and bake the final state back to Rhino for drawings. **The definition is
the source; the baked geometry is an output.** Never edit baked geometry by
hand and then expect the definition to know.

## 10. Habits that pay for themselves

- **Name every slider** (double-click its label): `bay width`, not `Slider`.
  At the review I will ask you to change three parameters; you have to find them.
- **Group as you go** (`Ctrl` + `G`), one group per logical step, and name
  it. Week 15 is about the mess you do *not* make now.
- **Align as you go.** Select several components and line them up with the
  *Align* widget (Display ▸ Canvas Widgets). Straight rows read faster than
  scattered ones.
- **Scribble** a title and short notes on the canvas.
- **Save versions** (`facade_v03.gh`). A definition can break in a way
  `Ctrl` + `Z` does not undo.
- **When it is slow**, turn on the *Profiler* widget (Display ▸ Canvas
  Widgets) to see which component takes the time.

---

## Cheatsheet

| | |
| --- | --- |
| search / place | double-click canvas · type `0<5<10` for a ranged slider |
| where does it live? | `Ctrl` + `Alt` + press on the component |
| find on canvas | `Ctrl` + `F` |
| add / remove / move wires | `Shift` drag · `Ctrl` drag · `Ctrl` + `Shift` drag |
| wire display | right-click input ▸ Wire Display ▸ Default / Faint / Hidden |
| preview on/off · disable | `Ctrl` + `Q` · `Ctrl` + `E` |
| preview selected only | canvas-toolbar button |
| group | `Ctrl` + `G` |
| radial menu | middle-click |
| recompute | `F5` |
| reference · internalise · bake | right-click ▸ Set one/multiple · Internalise data · Bake |
| debug | a Panel, with Draw Indices on |
| colours | grey fine · orange warning · red error |
| wires | single item · double list · dashed tree |

## In the room

No build this week. A guided tour, then **the essentials drill**: the same
small flow (a point → a circle → an extruded cylinder) made with each of the
five point sources in §8, and a one-sentence argument for which one you would
keep. From Week 06 we build together, with polls (see
[how the builds work](/README.md#how-the-builds-work)).

## Homework

- Work through the drill until every row of the cheatsheet is in your hands, not on the page
- Your project variant is assigned this week: reference your strip into an empty definition and internalise it

## Commands

The commands this week centres on. If one of these is not covered by the prose above, that's a signal to teach it — the list here is the week's source of truth for what students walk in expecting to use.

```
_Grasshopper
Number Slider
MD Slider
Panel
Point
Construct Point
Curve
Circle
Extrude
Custom Preview
Scribble
Group
Bake
Internalise Data
```

## Reference

Read before class; we will not spend session time on it.

- [rccn wiki → grasshopper/interface-canvas-display](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/interface-canvas-display)
- [rccn wiki → grasshopper/data-types](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/data-types)
- [rccn wiki → grasshopper/interop-baking-attributes](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/interop-baking-attributes)
- [rccn wiki → getting-started](https://kb.rccn.dev/computation/rhino-grasshopper/getting-started)

---

Previous: [Week 04](/Lecture/Week_04/README.md) · Next: [Week 06](/Lecture/Week_06/README.md)
