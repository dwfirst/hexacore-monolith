# Origin

This document is the honest story of how HCM-1 came to be. No polish, no
marketing. Just the path.

---

## Where it started

In 2026 I began playing with local language models. The reality of my setup:
an Intel i3-1115G4, two cores, 16 GB of RAM, no GPU. Everything ran slow.
Painfully slow.

I started asking AI how to make local inference *cheap* — not fast, just
usable. That question pulled me into a rabbit hole that lasted months.

---

## The first idea — a swarm

My first concept was a **swarm**. Instead of one big machine, many small ones
working together.

I went through several iterations:

- **A swarm of phones** — old Android devices on Snapdragon chips, unified
  into a single AI brain by a **GL.iNet Beryl AX (GL-MT3000)** router. Each
  phone would take a slice of the work; the router would route tasks between
  them.
- **Single-board computers** — Orange Pi boards as nodes.
- **Bare motherboards** — Intel N100 mini-ITX boards.

None of them felt right. Each version was a patch over the real problem:
**you cannot fake a unified machine by stringing together separate ones.**

---

## The pivot — old server boards

Then I remembered old **multi-socket server motherboards** — 2 or 4 Pentium
processors on one board, sharing memory and I/O. That is when the idea
clicked:

**What if the whole thing was one unit, not many?**

Not a cluster. Not a network. A single substrate with everything on it.

---

## Long conversations with AI

I spent weeks talking to AI about materials, topologies, and physics. We
went through:

- **Bionics** — could a chip learn from biology?
- **Liquid crystals** — could compute happen in a fluid medium?
- **Quantum cores** — is there a future where quantum and classical share
  a die?

Most of those paths did not work. But one thought kept returning:

**Nature already solved the packing problem.**

---

## The bee

I was outside. A bee flew past. I watched it for a moment — and then it hit
me:

**The hexagon.**

Not a square. Not a triangle. A hexagon is the most efficient way to pack
identical cells with no wasted space. Bees found it millions of years ago.
Why not silicon?

I spent the next weeks digging into hexagonal topology — mesh networks, NoC
research, HexaTile benchmarks. It was not just beautiful. It was
**measurably better** than a square grid: less latency, less energy,
shorter paths.

---

## The sketch

Eventually I drew it. First sketch — five hexagons in a cross. It was wrong:
too hierarchical, the center too dominant.

Second sketch — **six hexagons around one center**. Perfect symmetry. Two
NPUs, two RAMs, one CPU, one GPU. Every chiplet one hop from the shared hub.

That is when I knew the shape was right.

---

## And then I came back to it

Months passed. Life happened. Then, in late 2026, I came back to the idea —
this time with a clearer purpose: not to build it, but to **write it down**
as a concept others could pick up.

That is what this repository is.

---

## What this document is not

It is not a technical justification. It is not a pitch. It is not a claim
that I invented anything.

It is just the path — from a slow laptop, through a swarm of dead ideas, to
a bee on a summer day, to six hexagons on a page.

The rest is downstream.
