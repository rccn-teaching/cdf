# Week 07 — goals

*A twisting tower* · 🔹 **Standalone build**

> A goal is a **data flow**, not a list of components. It says what has to
> happen, not how. Two people building the same goal will produce different
> definitions, and comparing them is the point.

You will not be given a `.gh` file for these. [Reading one teaches nothing and the building is the skill](https://kb.rccn.dev/computation/rhino-grasshopper/grasshopper/describing-a-definition).

---

## The goal

A 30-storey tower whose square floor plates rotate and taper upward, with a skin and, if we can, vertical mullions.

```mermaid
flowchart LR
    F0["one floor plate"]
    H1["floor heights"]
    M2["plates moved up"]
    R3["rotated + scaled per floor"]
    L4["lofted skin"]
    U5["mullions?"]
    F0 --> H1 --> M2 --> R3 --> L4 --> U5
```

## How we build it

We build stage by stage, together. At each 🗳️ I stop: everyone votes on what goes next, *then* we build it, and the options that lost get discussed, because a wrong answer you can explain is worth more than a right one you guessed. The answers are folded away below each poll. Open them after the vote, not before.

---

### Stage 1 — Stack the floors

```mermaid
flowchart LR
    F0["a square"]
    H1["Series of heights"]
    M2["Move along Z"]
    F0 --> H1 --> M2
```

> 🗳️ **Poll 1** — *We have one square and 30 heights. How do we get 30 squares?*
>
> **A.** Move, with a Series into the Z of a vector · **B.** Copy in Rhino 30 times · **C.** Array Linear · **D.** Loft

<details><summary>After the vote</summary>

**We take: Move, with a Series into the Z of a vector.** One geometry and a list of 30 vectors gives 30 results, because Grasshopper matches lists. Array Linear works too (and is worth knowing); copying in Rhino defeats the point of the session. Loft comes later and needs the curves first.

</details>

---

### Stage 2 — Twist and taper

```mermaid
flowchart LR
    M0["30 plates"]
    A1["angles: Series"]
    R2["Rotate about each centre"]
    S3["Scale"]
    M0 --> A1 --> R2 --> S3
```

> 🗳️ **Poll 2** — *Rotate needs a centre plane per floor. Where does it come from?*
>
> **A.** World XY plane · **B.** Area (its centroid) → a plane · **C.** a referenced point · **D.** the plate's start point

<details><summary>After the vote</summary>

**We take: Area (its centroid) → a plane.** Area returns each plate's centroid: 30 centres for 30 plates, computed, not typed. World XY rotates every floor about the ground origin and swings the tower off its base. A referenced point is one centre for all, which is only right while the plates are concentric.

</details>

---

### Stage 3 — Skin, then the cliffhanger

```mermaid
flowchart LR
    R0["twisted plates"]
    L1["Loft"]
    D2["Divide each plate into 12"]
    P3["Polyline through the points…"]
    R0 --> L1 --> D2 --> P3
```

> 🗳️ **Poll 3** — *We divide every plate into 12 points and want 12 vertical mullions. What do we connect?*
>
> **A.** Polyline straight from Divide Curve · **B.** Interpolate · **C.** Line · **D.** we need something else

<details><summary>After the vote</summary>

**We take: we need something else.** Wire Divide Curve straight into Polyline and you get 30 horizontal rings, not 12 verticals: the points are organised *by floor*, and we need them *by column*. Look at the wire: it has gone dashed. That is a **data tree**, and turning floors into columns is a tree operation. Next week. Leave the definition exactly as it is and bring it.

</details>

---

## After the session

Rebuild it on **your strip**, from the diagrams only. If it only works on the class example, you built a drawing with sliders attached.
