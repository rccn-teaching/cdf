# The Project — a facade system you can steer

> Released Week 04. Iterations due W11 and W14, freeze W16, review W18.
> This is 100% of your grade. There is no exam.

## The brief

**Design a facade system for a given building, and build the Grasshopper
definition that generates it.**

One building, one orientation problem, fifty solutions. The building is a
`TBC-STOREY` block on a real site — model supplied in
[`Project/base/`](/Project/base/). It is deliberately ordinary: the design work
is in the skin, not in the massing.

Your system must respond to something real. Sun, view, privacy, structure,
rainfall, the street, the neighbours — pick one and mean it. "It looks
interesting" is not a driver, and it is the first thing the review will test.

## Your variant

Each student gets a different **facade strip** — an elevation, a floor range and
a programme behind it — assigned in Week 05 and listed in
[`Project/variants.md`](/Project/variants.md).

This matters more than it looks. Because everybody solves the same *problem*,
every demo in every session applies to your work. Because everybody has a
different *strip*, nobody's solution is transferable and comparing yours to your
podmate's is genuinely informative.

South-facing strips have a shading problem. North-facing strips have a daylight
problem. A strip behind a stairwell barely has a problem at all and you will
have to argue for what it should do instead. These are not equal, deliberately —
part of the work is judging what your strip actually needs.

## What you hand in

```
Project/submissions/<your-student-id>/
├── definition.gh          the definition, internalised so it opens anywhere
├── model.3dm              the base model, your layers, one baked result
├── README.md              200 words: the driver, the logic, the decisions
├── drawings.pdf           elevation, section, one detail at 1:20
└── images/                three, minimum: system, close-up, in context
```

**The definition is the deliverable.** Everything else is evidence about it.

### The definition has to open

Internalise your inputs or reference geometry that ships in your folder. A
definition that only runs on your desktop is not finished. Test it: open it on
a lab machine, or a podmate's laptop, before you call it done.

It also has to be *readable*. Grouped, the groups labelled, the driving
parameters gathered where a stranger would look for them, no orphaned clusters
of dead components. Week 15 is about this and it is assessed.

## Milestones

| Week | Due | What is actually being checked |
| ---- | --- | --- |
| 04 | brief released | — |
| 05 | variant assigned | — |
| 08 | **concept review** — one sketch, one paragraph, one reference | Have you chosen a driver, or a shape you like? |
| 11 | **iteration 1** — the system generates, roughly, on your strip | Does it run end to end? Does changing an input change the right thing? |
| 14 | **iteration 2** — fabricable, panel schedule, unrolled | Is it true? Would it survive being built? |
| 16 | **freeze** — pod clinic, in front of everyone | Is anything still broken that you have been avoiding? |
| 18 | **final review** — driven live | Can you steer it, and explain why it is that way? |

Missing an iteration is not fatal. Arriving at Week 16 with a definition that
has never run end to end is.

## Assessment

No point breakdown. Five things, weighted by judgement:

1. **It runs.** The definition opens on another machine and generates the system.
2. **It is steerable.** The parameters that matter are exposed and named, and
   moving them does something sensible rather than exploding.
3. **It responds.** The system demonstrably answers the driver you chose. You
   can show the difference between your strip and a different one.
4. **It is buildable.** Panels unroll, the schedule adds up, nothing is 0.3 mm
   thick or intersecting itself.
5. **You can explain it.** Live, with the file open, including the parts you
   found hard — and you can make one unseen change to it in fifteen minutes.
   That is the [oral defence](/README.md#the-oral-defence), and it is the part
   no amount of help can be substituted into.

> **Process is worth more than the artefact.** A system that is honestly
> resolved and modestly ambitious beats a spectacular one you cannot open,
> cannot change, and cannot account for.

## The pattern library

Separately from the project, each of you contributes **one recipe** to
[`Project/library/`](/Project/library/) — a small, working, documented
definition solving one problem well. Fifteen components, not five hundred.

- due Week 15, reviewed by your pod before it lands
- a `README.md` leading with the flow diagram, plus the `.gh` and one image
- it may come out of your project, but it has to stand alone

Fifty of these is a genuinely useful library, and it is yours afterwards.
Contributing is part of the gate, not part of the grade.

## Pods

You are in a pod of five from Week 03. Pods review before I do.

- **Before every milestone**, your pod reads each other's work. Not "looks nice"
  — open the definition, change an input, try to break it.
- **One question per pod per week** comes to class, chosen by the pod. If four
  of you are stuck on the same thing, that is the question.
- **Clinics** (W11, W15, W16) are per-pod, in front of the room.

The reason to take this seriously: reviewing four other definitions will teach
you more about Grasshopper than building one. Reading is where the judgement
comes from.

## Groups

Individual. The pod is for review, not for shared work — every definition is
yours, and at the final review you are the only one who can answer for it.
