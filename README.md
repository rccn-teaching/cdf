# ARCH2022 Computational Design Fundamental

Rhino and Grasshopper for architectural design. The first quarter is **modelling
with intent**: what Rhino is actually good at, and how to build a model that
survives contact with a deadline. The rest is **Grasshopper**, taught as a
practical skill.

Two claims shape how this course runs.

**You do not learn software in a classroom. You learn it by using it on
something you care about.** Every hour of watching someone else model is worth
about ten minutes of doing it yourself. So the room is for the things you cannot
do alone — building alongside someone who is faster than you, having your work
looked at, and arguing about whether something is good. Reference material is
homework, because reading is something you are already able to do at your own
pace, at 2am, with the page open beside Rhino.

**Fluency is physical.** Nobody becomes good at Grasshopper by understanding it.
They become good by having built the same kind of thing enough times that their
hands go to the right component without asking. That is why most Grasshopper
sessions are **builds**, not lectures — see [Three goals](#three-goals).

* ARCH2022 · **WED 10:10-12:00** · Computer Lab

---

## Schedule

### Part I — Rhino: the anatomy, and how to drive it (W01–W04)

| Week | Topic | Concepts | Practice |
| ---- | ----- | -------- | -------- |
| **01** | **The anatomy of a Rhino model ⭐**<br>👉[Lecture](/Lecture/Week_01/README.md)<br>🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W01/) | · command line as the interface, hotkeys, aliases<br>· data types: point / curve / surface / poly* / mesh / SubD<br>· what a NURBS is — control points, degree, knots<br>· every surface is a rectangle; trimming stores a mask<br>· join, polysurface, and "solid" is not a type<br>· units and tolerance, and why booleans fail<br>· nested layers, lock, colour, print width<br>· named views, F6 camera, CPlane + Plan | Set up · model one closed solid · trim + Untrim demo · save 3 named views · [self-check](/SELF-CHECK.md) clean |
| **02** | **Making things: curves into surfaces**<br>👉[Lecture](/Lecture/Week_02/README.md)<br>🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W02/) | · InterpCrv vs Curve: through-points vs pulled-toward<br>· continuity: G0 touch, G1 tangent, G2 matching curvature<br>· surfaces are as good as the curves under them<br>· which surface command, and when<br>· trim, split, join, cap — and what breaks each | Rebuild W01 element from clean curves · one double-curved surface passing `Zebra` · one filleted solid |
| **03** | **Working at scale**<br>👉[Lecture](/Lecture/Week_03/README.md)<br>🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W03/) | · the `Sel*` family; window vs crossing selection<br>· naming, and why Grasshopper will care from W05<br>· blocks: when worth it, when ceremony<br>· referencing versus copying the site file<br>· model hygiene as a routine, not a hand-in step<br>· what to model and what to fake | Reorganise into numbered nested layers · one block placed ≥3× · name what GH will need · **pods form** |
| **04** | **Getting it out**<br>👉[Lecture](/Lecture/Week_04/README.md)<br>🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W04/) | · Make2D is static and slow; tangent-edges matter<br>· annotation styles, and `Dot` for panel numbers later<br>· layouts, details, per-detail scale + lock<br>· print width per layer, independent of screen<br>· `ViewCaptureToFile` with a deliberate display mode<br>· unrolling — developable vs not | One sheet (plan/elev/section, stated scale, PDF) · one 2000 px+ image · one element unrolled · 🎓 **brief released** |

### Part II — Grasshopper: the fundamentals (W05–W10)

The weeks people find hardest, in the order that hurts least. Data trees get
two weeks because one is a lie.

| Week | Topic | Concepts | Practice |
| ---- | ----- | -------- | -------- |
| **05** | **The canvas and the flow**<br>👉[Lecture](/Lecture/Week_05/README.md)<br>🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W05/) | · params vs components; what a wire carries<br>· referencing Rhino geometry — internalise from day one<br>· the panel is the only debugger you get<br>· group and name as you build | Three [goals](/Lecture/Week_05/goals.md) · **variant assigned** |
| **06** | **Lists, ranges, and the index**<br>👉[Lecture](/Lecture/Week_06/README.md)<br>🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W06/) | · `Series` vs `Range` — pick the right one<br>· indexing, negative indices, going past the end<br>· the index as a design parameter | Three [goals](/Lecture/Week_06/goals.md) · drive one thing in your strip by index |
| **07** | **Data trees I — what a path is**<br>👉[Lecture](/Lecture/Week_07/README.md)<br>🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W07/) | · `{0;1;2}` is a sentence — read it out loud<br>· inputs decide the output's structure<br>· matching: shortest, longest, cross-reference<br>· read the tree *before* fixing it | Three [goals](/Lecture/Week_07/goals.md) · Param Viewer in 3 places in your definition |
| **08** | **Data trees II — graft, flatten, and the honest fix**<br>👉[Lecture](/Lecture/Week_08/README.md)<br>🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W08/) | · what graft/flatten/simplify actually do to paths<br>· the flatten reflex hides bugs it does not fix<br>· `Path Mapper` is a last resort — something upstream is wrong<br>· diagnose as a tree problem, not a geometry problem | Three [goals](/Lecture/Week_08/goals.md) · 🎓 **concept review** (sketch + paragraph + reference) |
| **09** | **Curves and surfaces, parametrically**<br>👉[Lecture](/Lecture/Week_09/README.md)<br>🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W09/) | · the `t` parameter; reparameterising to 0–1<br>· surface UV — the Week 01 rectangle again<br>· frames and planes — orient without fighting<br>· trims are masks; surface components see the rectangle | Three [goals](/Lecture/Week_09/goals.md) · W02 surface returns, driven parametrically |
| **10** | **Attractors, remapping, fields**<br>👉[Lecture](/Lecture/Week_10/README.md)<br>🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W10/) | · distance as a driver — point, curve, surface attractors<br>· `Remap Numbers`: name both domains out loud<br>· shape a falloff deliberately with `Graph Mapper`<br>· is the variation *doing* anything? | Three [goals](/Lecture/Week_10/goals.md) · choose a driver for your strip, defend it |

### Part III — Grasshopper: systems (W11–W15)

| Week | Topic | Concepts | Practice |
| ---- | ----- | -------- | -------- |
| **11** | **Panelisation and subdivision**<br>👉[Lecture](/Lecture/Week_11/README.md)<br>🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W11/) | · quad, triangular, diamond, hexagonal grids<br>· planarity: quads on a double-curved surface are not flat<br>· panel numbering — identity through the pipeline<br>· the seam and the pole — where a surface betrays you | 🎓 **iteration 1** — the system generates, roughly, on your strip |
| **12** | **Meshes, and when not to use NURBS**<br>👉[Lecture](/Lecture/Week_12/README.md)<br>🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W12/) | · mesh vs NURBS — what each is good at, what each costs<br>· topology: vertices, faces, naked edges, welding<br>· when to convert, in which direction<br>· meshes from scans and surveys | Three [goals](/Lecture/Week_12/goals.md) · decide *in writing* which your system uses |
| **13** | **Form-finding**<br>👉[Lecture](/Lecture/Week_13/README.md)<br>🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W13/) | · relaxation as a method, not an effect<br>· anchors and springs; reading a solver that will not settle<br>· form as a consequence of physical constraints | Three [goals](/Lecture/Week_13/goals.md) · take it into the project if it fits |
| **14** | **Fabrication prep: unroll, nest, label**<br>👉[Lecture](/Lecture/Week_14/README.md)<br>🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W14/) | · unrolling from Grasshopper; developable vs not<br>· nesting, sheet efficiency, material constraints as inputs<br>· labelling — identity surviving to the cut file<br>· tolerance and kerf: the gap between model and machine | 🎓 **iteration 2** — fabricable, scheduled, unrolled |
| **15** | **Definition hygiene and performance**<br>👉[Lecture](/Lecture/Week_15/README.md)<br>🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W15/) | · group, name, colour — lay out a definition to be read<br>· internalise data; make the file open elsewhere<br>· what is actually slow: previews, recomputation, huge trees<br>· the review question: could someone else drive this? | Clean your definition for a reader · 📚 **library recipe** · pod review |


### Part IV — Build (W16–W18)

| Week | Session | Milestone |
| ---- | ------- | --------- |
| 16 | 🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W16/) · **Pod clinic** — rotating, 15 minutes per pod, in front of everyone. | 🎓 **freeze** |
| 17 | **Production** — drawings, images, the definition cleaned for a reader. Defences begin, by pod.<br>🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W17/) | 📝 **defences (A + B)** |
| 18 | 🎓 **Final review** — the definition driven live, and the question answered out loud.<br>🎬[Slides](https://slides.rccn.dev/courses/CDF/CDF-W18/) | 🎓 **submission** · 📝 review due |

---

## How this course is assessed

**The project is your grade — 100%.** There is no exam nor roll-call

The Rhino work in Weeks 01–05 is not scored, but it is a **required gate**: your
Week 05 model becomes your project base, and everything after Week 06 assumes a
model you can trust. Check it yourself with [SELF-CHECK.md](/SELF-CHECK.md).

The criteria are in the [project brief](/Project/README.md#assessment). The theme
throughout: **the definition is the deliverable, not the render.** A beautiful
image from a definition nobody can open or change is worth less here than a
plain one a stranger could pick up and steer.

### The oral defence

The project is assessed with the file open, in front of you.

- I name **three parameters**. Change them, and say what should happen *before*
  it does
- I point at **one component**. Why is it there? What breaks without it?
- One change you have not seen, made live, in fifteen minutes

That last part is the course question turned around. All term it has been *could
someone else drive this?* At the review: **can you?**

You will have had an assistant, a forum and fifty tutorials open all semester,
and so will everyone you ever work with. Pretending otherwise would measure your
willingness to play along rather than your ability. So the position is simple:
