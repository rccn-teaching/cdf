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
sessions are **builds**, not lectures — see [how the builds work](#how-the-builds-work).

* ARCH2022 · **WED 10:10-12:00** · Computer Lab

---

## Schedule

### Part I — Rhino: the anatomy, and how to drive it (W01–W04)

| Week | Topic | Concepts | Practice |
| ---- | ----- | -------- | -------- |
| **01** | **The anatomy of a Rhino model ⭐**<br>👉[Lecture](/Lecture/Week_01/README.md) | · command line as the interface, hotkeys, aliases<br>· data types: point / curve / surface / poly* / mesh / SubD<br>· what a NURBS is — control points, degree, knots<br>· every surface is a rectangle; trimming stores a mask<br>· join, polysurface, and "solid" is not a type<br>· units and tolerance, and why booleans fail<br>· nested layers, lock, colour, print width<br>· named views, F6 camera, CPlane + Plan | Set up · model one closed solid · trim + Untrim demo · save 3 named views · [self-check](/SELF-CHECK.md) clean |
| **02** | **Making things: curves into surfaces**<br>👉[Lecture](/Lecture/Week_02/README.md) | · InterpCrv vs Curve: through-points vs pulled-toward<br>· continuity: G0 touch, G1 tangent, G2 matching curvature<br>· surfaces are as good as the curves under them<br>· which surface command, and when<br>· trim, split, join, cap — and what breaks each | Rebuild W01 element from clean curves · one double-curved surface passing `Zebra` · one filleted solid |
| **03** | **Working at scale**<br>👉[Lecture](/Lecture/Week_03/README.md) | · the `Sel*` family; window vs crossing selection<br>· naming, and why Grasshopper will care from W05<br>· blocks: when worth it, when ceremony<br>· referencing versus copying the site file<br>· model hygiene as a routine, not a hand-in step<br>· what to model and what to fake | Reorganise into numbered nested layers · one block placed ≥3× · name what GH will need · **pods form** |
| **04** | **Getting it out**<br>👉[Lecture](/Lecture/Week_04/README.md) | · where Rhino stops — fast draft and fabrication, not BIM, not Illustrator<br>· SubD: sculpt a form with it, rebuild as NURBS to draft it<br>· Make2D is static and slow; maintain source layers<br>· clipping sections + section styles — poché that updates with the model<br>· layouts, details, per-detail scale + lock, aligning drawings<br>· print colour + width per layer; `PrintDisplay` is off by default<br>· linetypes, non-printing layers, vector PDF out to Illustrator<br>· annotation styles, and `Dot` for panel numbers later<br>· `ViewCaptureToFile` with a deliberate display mode<br>· unrolling — developable vs not | One sheet (plan/elev/section, stated scale, vector PDF) · one 2000 px+ image · one element unrolled · 🎓 **brief released** |

### Part II — Grasshopper: the fundamentals (W05–W10)

Week 05 is the operating manual. From Week 06 every session is a **live build** ([how the builds work](#how-the-builds-work)). Data trees get **one** week, Week 08, placed *after* two builds have run into them, so there is something real to fix.

| Week | Topic | Concepts | Practice |
| ---- | ----- | -------- | -------- |
| **05** | **Grasshopper essentials**<br>👉[Lecture + cheatsheet](/Lecture/Week_05/README.md) | · the window, params vs components, what colours and wires tell you<br>· search, place, wire; obscure components; find on canvas<br>· preview, preview-selected-only, disable, wire display<br>· reference, internalise, bake<br>· five ways to make a point, and when each is right<br>· Rhino or Grasshopper? | the essentials [drill](/Lecture/Week_05/goals.md) · **variant assigned** |
| **06** | **Lists, ranges, and the index**<br>👉[Lecture](/Lecture/Week_06/README.md) · [build](/Lecture/Week_06/goals.md) | · `Series` vs `Range`, and picking the right one<br>· indexing: negative indices, going past the end, wrapping<br>· the index as a design parameter: every *n*th bay is different<br>· list length as the first sanity check | 🧱 build 1 · drive one thing in your strip by index |
| **07** | **A twisting tower**<br>👉[Lecture](/Lecture/Week_07/README.md) · [build](/Lecture/Week_07/goals.md) | · a floor plate repeated by `Series`: heights as a list<br>· rotation and scale *per floor*: two lists that must line up<br>· lofting through a list of curves<br>· the moment one list becomes many: points on every floor | 🔹 standalone · ends on a tree cliffhanger |
| **08** | **Data trees: one week, on real problems**<br>👉[Lecture](/Lecture/Week_08/README.md) · [build](/Lecture/Week_08/goals.md) | · `{0;1;2}` is a sentence: read it out loud<br>· how a component's inputs decide its output's structure<br>· Graft, Flatten, Simplify, Flip Matrix: what each does to the paths<br>· matching: shortest list, longest list, cross reference<br>· the flatten reflex hides bugs; Path Mapper is a last resort | 🌳 concept · 🎓 **concept review** (sketch + paragraph + reference) |
| **09** | **Curves and surfaces, parametrically**<br>👉[Lecture](/Lecture/Week_09/README.md) · [build](/Lecture/Week_09/goals.md) | · the `t` parameter, and reparameterising to 0–1<br>· surface UV: the Week 01 rectangle again<br>· frames and planes: orient without fighting<br>· trims are masks, and surface components see the untrimmed rectangle | 🧱 build 2 · louvres on your strip's surface |
| **10** | **A perforated screen: attractors and fields**<br>👉[Lecture](/Lecture/Week_10/README.md) · [build](/Lecture/Week_10/goals.md) | · distance as a driver: point, curve and surface attractors<br>· `Remap Numbers`: name both domains out loud<br>· shaping a falloff deliberately with `Graph Mapper`<br>· is the variation *doing* anything? | 🔹 standalone · choose a driver for your strip, defend it |

### Part III — Grasshopper: systems (W11–W15)

| Week | Topic | Concepts | Practice |
| ---- | ----- | -------- | -------- |
| **11** | **Panelisation**<br>👉[Lecture](/Lecture/Week_11/README.md) · [build](/Lecture/Week_11/goals.md) | · quad, diamond and triangular panels<br>· planarity: quads on a double-curved surface are not flat<br>· panel numbering: identity through the pipeline<br>· the seam and the pole: where a surface betrays you | 🧱 build 3 · 🎓 **iteration 1** — the system generates, roughly, on your strip |
| **12** | **A site from survey points: meshes**<br>👉[Lecture](/Lecture/Week_12/README.md) · [build](/Lecture/Week_12/goals.md) | · mesh vs NURBS: what each is good at, what each costs<br>· topology: vertices, faces, naked edges, welding<br>· when to convert, and in which direction<br>· meshes from scans and surveys | 🔹 standalone · decide *in writing* NURBS or mesh |
| **13** | **A hanging canopy: form-finding**<br>👉[Lecture](/Lecture/Week_13/README.md) · [build](/Lecture/Week_13/goals.md) | · relaxation as a method, not an effect<br>· anchors and springs; reading a solver that will not settle<br>· form as a consequence of physical constraints | 🔹 standalone · take it into the project if it fits |
| **14** | **Fabrication prep: flatten, label, lay out**<br>👉[Lecture](/Lecture/Week_14/README.md) · [build](/Lecture/Week_14/goals.md) | · laying planar panels flat; unrolling what is not planar<br>· nesting, sheet efficiency, and material constraints as inputs<br>· labelling: identity surviving to the cut file<br>· tolerance and kerf: the gap between model and machine | 🧱 build 4 · 🎓 **iteration 2** — fabricable, scheduled, unrolled |
| **15** | **Make it readable, make it fast**<br>👉[Lecture](/Lecture/Week_15/README.md) · [build](/Lecture/Week_15/goals.md) | · group, name, colour: lay out a definition to be read<br>· internalise data; make the file open elsewhere<br>· what is actually slow: previews, recomputation, huge trees<br>· the review question: could someone else drive this? | 🧱 build 5 · clean your definition for a reader · 📚 **library recipe** · pod review |


### Part IV — Build (W16–W18)

| Week | Session | Milestone |
| ---- | ------- | --------- |
| 16 | 🎬[Slides]() · **Pod clinic** — rotating, 15 minutes per pod, in front of everyone. | 🎓 **freeze** |
| 17 | **Production** — drawings, images, the definition cleaned for a reader. Defences begin, by pod. | 📝 **defences (A + B)** |
| 18 | 🎓 **Final review** — the definition driven live, and the question answered out loud. | 🎓 **submission** · 📝 review due |

---

## How the builds work

From Week 06 to Week 15 the session *is* a build: one definition, made live, by
everyone at once. Two kinds alternate:

- 🧱 **The class build** (W06, 09, 11, 14, 15): one facade system on the base
  building, growing a stage each time: bays, then louvres on the surface, then
  panels, then cut sheets, then a definition fit for a stranger. It is the
  project's own problem, solved once in front of you, so you can rebuild it on
  your strip.
- 🔹 **Standalone builds** (W07, 10, 12, 13): a tower, a screen, a terrain, a
  canopy. Each is self-contained and practises one family of ideas away from the
  facade, so the skill is not tied to one example.

Week 08 is the 🌳 **concept week**: data trees, taught on the problems the first
two builds actually produced.

**The polls.** At each critical point in a build (marked 🗳️ in that week's
`goals.md`), I stop and ask *which component do we place next?* Everyone votes
live, on `TBC-POLL-TOOL`, before anyone touches the canvas. Then we build the
winner and argue about the losers, because the wrong options are where the
understanding is. The answers sit folded away under each poll in `goals.md`.
Reading them early only spoils your own practice.

**After the session**, rebuild it on your own strip from the data-flow diagrams
alone. You will not be given a `.gh` file: [reading one teaches nothing, and the
building is the skill](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition).

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
