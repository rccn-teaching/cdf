# Week 06 — Lists, ranges, and the index

🧱 **Class build** · part 1 of 5

The class facade begins: from a strip of the base building to a grid of bays, and the index as a design parameter.

## What this session covers

- `Series` vs `Range`, and picking the right one
- indexing: negative indices, going past the end, wrapping
- the index as a design parameter: every *n*th bay is different
- list length as the first sanity check
- one component, many items: a list in, a list out

## In the room

The session has **two halves**, and the first exists to set up the second.

**First half: one example, walked through.** *A south strip of the base
building, divided into structural bays; every third bay gets a different
louvre spacing.* We build it together, live, from the data flow in
[`goals.md`](/Lecture/Week_06/goals.md). At **3 critical points** I stop and
you vote on what we place next (🗳️ in `goals.md`, polls run on
`TBC-POLL-TOOL`), then we argue about the result before anyone touches the
canvas. See [how the builds work](/README.md#how-the-builds-work). While we
build, watch the **wires**: at some point one thing becomes many.

**Second half: the list, taken apart.** Everything the example did, it did
to a *list*. Now we slow down and look at the list itself: what an index is,
why the count is always one off from what you expected, how to take a list
apart and put it back. Five short rounds of *predict, then check with a
Panel* ([`goals.md`, second half](/Lecture/Week_06/goals.md#second-half--the-list-taken-apart)),
with a vote before each check.

Keep the [**list cheatsheet**](/Lecture/Week_06/cheatsheet.md) open beside the
canvas. It is this week's one page of reference, written out because the rest
of the term stands on it.

You will not be given a `.gh` file. [Reading one teaches nothing, and the building is the skill](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition).

## Homework

- Rebuild the class definition on **your** strip, without looking
- Do the five rounds of the second half again, alone, on your own strip's edge: predict first, then Panel
- Drive one thing in your strip by index, and write one sentence on why that index

## Commands

The commands this week centres on. If one of these is not covered by the prose above, that's a signal to teach it — the list here is the week's source of truth for what students walk in expecting to use.

```
Series
Range
Divide Length
Divide Curve
List Item
List Length
Cull Pattern
Cull Index
Shift List
Dispatch
Weave
Sort List
Reverse List
Split List
Merge
```

## Reference

Read before class; we will not spend session time on it.

- [the list cheatsheet](/Lecture/Week_06/cheatsheet.md) (this week's page)
- [rccn wiki → grasshopper/data-types](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/data-types)
- [rccn wiki → grasshopper/numbers-logic-expressions](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/numbers-logic-expressions)
- [rccn wiki → grasshopper/describing-a-definition](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition)

---

Previous: [Week 05](/Lecture/Week_05/README.md) · Next: [Week 07](/Lecture/Week_07/README.md)
