# HexaCore Monolith-1

> A speculative processor architecture: six heterogeneous chiplets arranged in
> hexagonal symmetry around a shared central hub — interconnect, L4 cache, and
> power delivery in one place.

**Status:** concept / design fiction. Not engineering-ready. No fab partnership.

---

## Why this exists

Modern processors are hitting a wall. Not a wall of transistors — a wall of
*interconnect*. Data still travels too far between CPU, GPU, NPU, and memory.
Every millimeter costs latency, energy, and heat.

HCM-1 is a thought experiment: **what if the layout itself solved the problem?**

Six chiplets. One center. Hexagonal symmetry. The shortest possible paths
between everything that needs to talk.

---

## The architecture

**Six chiplets. One center. Hexagonal symmetry.**

At the center sits a single **HUB** node combining three functions:
interconnect routing, a shared **L4 cache**, and **power delivery**.

Around it, six chiplets in perfect hexagonal symmetry:

- **CPU** — general compute
- **GPU** — matrix and graphics
- **NPU 1** and **NPU 2** — neural inference (symmetric pair)
- **RAM 1** and **RAM 2** — 128 GB DDR7-class each, 256 GB total

Every chiplet connects **directly to the HUB** — never chiplet-to-chiplet.
This keeps the longest path in the system to exactly **two hops**. No chiplet
is more than one hop from the shared cache.

Interconnect uses **UCIe** — the emerging die-to-die standard. Packaging is
**2.5D silicon interposer**. Peripheral I/O (SSD, LAN, power) lives on a
carrier PCB, not inside the module.

### Structure

```mermaid
graph TD
    HUB(("HUB<br/>Interconnect<br/>L4 Cache<br/>Power Delivery"))
    CPU["CPU<br/>General compute"]
    GPU["GPU<br/>Matrix / graphics"]
    NPU1["NPU 1<br/>Neural inference"]
    NPU2["NPU 2<br/>Neural inference"]
    RAM1["RAM 1<br/>128 GB DDR7-class"]
    RAM2["RAM 2<br/>128 GB DDR7-class"]

    HUB --- CPU
    HUB --- GPU
    HUB --- NPU1
    HUB --- NPU2
    HUB --- RAM1
    HUB --- RAM2
Visualization prompt
Paste this into any AI image or diagram generator (Claude, GPT, Midjourney,
DALL·E, Stable Diffusion) to render the architecture.

A minimalist technical diagram of a processor module. At the center, a single
hexagonal node labeled HUB containing three stacked layers: interconnect,
L4 cache, power delivery. Around the HUB, six smaller hexagonal chiplets
arranged in perfect hexagonal symmetry — one at each vertex and one at each
edge midpoint. The chiplets are labeled CPU, GPU, NPU 1, NPU 2,
RAM 1, RAM 2. Thin straight lines connect every chiplet directly to
the HUB — no chiplet-to-chiplet lines. Style: engineering blueprint, dark
background (#0a0e14), thin cyan lines (#7dd3fc), monospace labels, no
decoration, no text beyond the labels. Flat 2D top-down view.

Design principles
Geometry before power. Fix the layout first — the shortest paths win.

Symmetry over hierarchy. Two NPUs and two RAMs are paired, not
subordinate. The hub is a peer, not a master.

Shared, not duplicated. A single L4 cache beats six private caches
that need to be kept coherent.

Fractal at every level. Hexagon at the module, hexagon at the die,
hexagon at the core. The pattern repeats because it works.

Speculative, not deceptive. This is design fiction with real physics
underneath. Not a pitch, not a product.

What is real, what is speculative
Real — already shipping in industry:

Hexagonal topology has measurable advantages over square mesh. HexaTile
(2026): −28.9% network diameter, −31.2% average latency, −34.2% energy-delay
product.

UCIe chiplet interconnect. AMD Versal RF: up to 6 links per package,
multi-terabit aggregate bandwidth.

Shared L4 / unified LLC between compute blocks. Intel and AMD both do
this already.

2.5D silicon interposer as packaging. AMD EPYC, Intel Xeon, Apple
M-series.

Palladium as a gold substitute in interconnects. Nornickel (2026):
3× cheaper, half the weight, melting point 1555°C.

Speculative — beyond current products:

Six-die hexagonal symmetry as a single coherent module. Closest analog is
AMD's multi-CCD layout, but not with a shared center hub.

Central hub combining interconnect, L4, and power delivery in one block.

256 GB of DDR7-class memory integrated at this density.

Where this could go — HCM-2
HCM-1 is the shape. HCM-2 will be the argument: a longer paper with
citations, comparison tables, and a realistic build path — which fabs,
which packaging vendors, which budgets.

If HCM-1 is a sketch on paper, HCM-2 is the blueprint.

What this is not
Not a startup pitch.

Not a claim that this can be built tomorrow.

Not a replacement for any existing product.

Not a promise of performance numbers.

It is a concept in system architecture — a direction for others to build,
critique, or ignore.

If you're building something like this
I don't write the RTL. I describe what the RTL should become.

If you're an engineer, a fab, or a research group working on chiplet
integration, hexagonal NoC, or speculative computer architecture — I'd like
to be in the room.

Open an issue or reach out.
