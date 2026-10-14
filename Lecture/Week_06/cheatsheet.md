# Week 06 — the list cheatsheet

*One page. Keep it open beside the canvas, next to the
[Week 05 cheatsheet](/Lecture/Week_05/README.md#cheatsheet).*

In Rhino you had **one** thing at a time: a curve, a surface. In Grasshopper a
single wire usually carries **many**: thirteen points, forty louvres. They
travel together in a **list**, and almost every question you will ask this term
is a question about a list: *how many? which one? in what order?*

Data trees are not on this page. They are Week 08.

---

## 1. What a list is

A numbered row of boxes. Three facts, and the rest of the page follows from
them:

```
index     0     1     2     3     4            the position: starts at 0
item     pt    pt    pt    pt    pt            the thing in the box
                                               length = 5, last index = 4
```

- An **item** is one thing. A **list** is items in an order.
- The **index** is an item's position. **It starts at 0.**
- The **length** is how many items. The last index is always **length − 1**.

**The order is real.** Divide a curve and the points come out in the curve's
direction, so index 0 is at the curve's start. Flip the curve in Rhino
(`_Flip`, or `_Dir` to see it) and every index reverses.

## 2. Read it before you use it

| To find out | Do this |
| --- | --- |
| is it one item, or a list? | look at the **wire**: single line = one item, double line = a list (dashed = a tree: stop, Week 08) |
| what is in it, and at which index? | wire it into a **Panel** (the index is the small number on the left) |
| how many? | **List Length**, or hover the output and read the tooltip |
| where is item *n* in the model? | **List Item** with a slider on `i`, and watch the preview move |

> **Length first.** Before wiring a list into anything, know its length and
> say the number you expect. "Thirteen points, so twelve bays." If the panel
> disagrees with you, one of you is wrong, and it is cheaper to find out now.

**The fence-post rule.** *n* gaps have *n + 1* posts. An 18 m edge at 1.5 m
bays has 12 bays and **13** points. Most off-by-one mistakes this term are
this one.

## 3. Making a list

| You know | Use | You get |
| --- | --- | --- |
| a **start**, a **step**, and **how many** | **Series** (S, N, C) | exactly **C** numbers: 0, 1.5, 3.0 … It does not know where to stop, only how many |
| the **two ends**, and how many **steps** between | **Range** (D, N) | **N + 1** numbers, both ends included. Fence posts again |
| a **curve**, and a **spacing** | **Divide Length** | a point every so many metres from the start. Whatever is left over at the end stays empty |
| a **curve**, and a **count** | **Divide Curve** (N) | N equal segments, so **N + 1** points on an open curve |

Know the **step**: Series. Know the **ends**: Range. Know the **spacing**:
Divide Length. Know the **count**: Divide Curve. *Which number is the given
decides the component.*

## 4. Taking one out

**List Item** (L, i, Wrap) picks the item at index `i`.

| `i` on a list of 13 | Wrap **on** (the default) | Wrap **off** |
| --- | --- | --- |
| `0` | the first | the first |
| `12` | the last | the last |
| `13` | back round to the **first** | red: index out of range |
| `-1` | the **last** | red |

Wrap is why a pattern can run round a closed facade without a seam. It is also
why a wrong index can give you *an* answer instead of an error. Zoom in on
List Item and a `+` appears: extra outputs for the next and previous items.

## 5. Splitting a list

A **pattern** is a short list of true/false that repeats until the list runs
out. `True, False, False` means *yes, no, no, yes, no, no …*, so indices
0, 3, 6, 9 … are the *yes*.

| Component | What comes out |
| --- | --- |
| **Dispatch** (L, P) | **two** lists: A where the pattern is true, B where it is false. Nothing is lost |
| **Cull Pattern** (L, P) | **one** list: the true ones. The rest are gone |
| **Cull Index** (L, I) | the list **without** the indices you name |
| **Split List** (L, i) | everything before index `i`, and everything from `i` on |

Need both halves later? **Dispatch.** Need only one? **Cull.**
Check: the lengths of A and B must add up to the length you started with.

## 6. Reordering and recombining

| Component | What it does | Typical use |
| --- | --- | --- |
| **Shift List** (L, S, Wrap) | moves the start: shift 1 makes item 1 the new item 0 | pair every point with **the next one**: the original list and the list shifted by 1 |
| **Reverse List** | last becomes first | when the curve ran the wrong way |
| **Sort List** (K, A) | sorts the numbers in K, and reorders A **the same way** | order panels by height, bays by distance to something |
| **Weave** (P, 0, 1) | deals items back together from two lists, following a pattern | the opposite of Dispatch: change one half, weave it back |
| **Merge** | one list after the other | join two streams end to end |

Shift List with **wrap off** drops what falls off the end, so the result is
one shorter: 13 points become 12. Twelve is the number of bays. That is not a
coincidence.

## 7. The index is a design parameter

"Every third bay is different" is a sentence about **indices**, not about
geometry. Once the bays are a list, decisions like these are one small list
of true/false, or one number:

- every *n*th one: a pattern of length *n*
- the first and the last: indices `0` and `-1`
- the ones near the corner: the first few (Split List)
- alternate, but starting one later: the same pattern, **shifted**

If you can say which indices, you can build it.

## 8. One component, many items

Give a component a **list** and it runs **once per item**: 13 points and one
radius make 13 circles. The single radius is used every time.

Two lists pair up **by index**: item 0 with item 0, item 1 with item 1. Keep
the two lists the **same length**, and check with List Length before you wire
them. What Grasshopper does when they differ is the first thing Week 08
explains; until then, make them match.

## 9. When it looks wrong

| You see | Usually |
| --- | --- |
| one too many, or one too few | fence posts (§2): points vs bays, N vs N + 1 |
| everything is right but mirrored, or the pattern starts at the wrong end | the curve's direction (§1). Flip it, or Reverse List |
| the pattern is right but one bay off | Shift List by 1, or start the pattern differently |
| an orange component and an empty panel | the list coming in is empty. Walk left until a panel shows data |
| a red List Item | index past the end, with Wrap off |
| a **dashed** wire where you expected a double one | a tree. Do not flatten it to make it go away. Note where it appeared and bring it to Week 08 |

---

## The short version

| | |
| --- | --- |
| index | starts at **0** · last = length − 1 · `-1` is the last (Wrap on) |
| read it | wire: single / double · **Panel** · **List Length** |
| fence posts | *n* gaps, *n + 1* points |
| make | step → **Series** (C numbers) · ends → **Range** (N + 1 numbers) |
| divide | spacing → **Divide Length** · count → **Divide Curve** (N + 1 points) |
| pick one | **List Item** (Wrap!) |
| split | keep both → **Dispatch** · keep one → **Cull Pattern** / **Cull Index** |
| pattern | repeats by itself: `T, F, F` = indices 0, 3, 6 … |
| reorder | **Shift List** · **Reverse List** · **Sort List** (keys drive values) |
| rejoin | **Weave** · **Merge** |
| neighbours | the list, and the list shifted by 1 |
| two lists | pair by index. Same length, or wait for Week 08 |

More, with pictures: [rccn wiki → grasshopper/data-types](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/data-types).

---

Back to [Week 06](/Lecture/Week_06/README.md) · the build: [`goals.md`](/Lecture/Week_06/goals.md)
