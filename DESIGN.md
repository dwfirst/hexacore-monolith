# Design

Technical companion to the main README. This is where the shape becomes
specific — topology, interconnect, materials, cooling.

**Status:** concept. Not engineering-ready. Numbers here are design targets,
not measured results.

---

## 1. Topology — why a hexagon

A square grid has four neighbours per node. A hexagonal grid has **six**, all
at equal distance. In a 2D layout, this is the most efficient way to pack
identical cells without wasted space — the "honeycomb" result, known since
ancient times and rediscovered by materials science many times over.

On a chip, this matters. Real research (HexaTile, 2026) compares hexagonal
NoCs to square mesh:

- Network diameter: **-28.9%**
- Average hop latency: **-31.2%**
- Energy-delay product: **-34.2%**

In HCM-1 the hexagon appears at every level:

- **Module** — six chiplets around one central hub
- **Chiplet** — hexagonal core clusters inside each die
- **Core** — hexagonal arrangement of execution units

The same shape at every scale, because the same packing problem appears at
every scale.

---

## 2. The Hub

The central node is the single most important design decision in HCM-1. It
combines three functions that are usually separate:

- **Interconnect routing** — every chiplet-to-chiplet path goes through here
- **Shared L4 cache** — a single coherent cache pool, not six private caches
- **Power delivery** — local regulation, distributed to the six chiplets

**Why one block?**

Because splitting them costs latency. If interconnect, cache, and power sit
in three different places, every transaction pays three coordination costs.
In one block, they pay one.

The hub is not a "master". It is a **peer** — it does not compute, it
coordinates. The CPU chiplet is not above the others; it is one of six.

---

## 3. Interconnect — UCIe

Chiplets are connected using **UCIe** (Universal Chiplet Interconnect
Express) — the emerging industry standard for die-to-die communication.

**Why UCIe:**

- It is an **open standard**, not a vendor lock-in
- It targets **sub-2 ns latency** across die boundaries
- It runs on standard **2.5D silicon interposers**
- Industry adoption: AMD, Intel, ARM, TSMC, Samsung all participate

Every chiplet connects **directly to the hub** — never chiplet-to-chiplet.
This keeps the longest path in the system to exactly **two hops**. No chiplet
is more than one hop from the shared L4.

---

## 4. Memory — 256 GB DDR7-class

Two RAM chiplets, 128 GB each. Positioned opposite each other in the
hexagon, so memory latency is symmetric from the hub's point of view.

**Why 256 GB:**

- Large enough for full local inference of a 70B-parameter model in 4-bit
  quantisation, with room for KV cache
- Distributed across two chips, so no single die carries the whole thermal
  load
- "DDR7-class" is a design target, not a shipping part. DDR7 does not exist
  in 2026; DDR6 is expected around 2028. This concept assumes a future
  generation with roughly 2x DDR6 bandwidth.

---

## 5. Materials

**Conductors — palladium instead of gold.**

Gold has been the default for high-reliability interconnects for decades.
Palladium is now a serious alternative:

- **3x cheaper** than gold (Nornickel, 2026)
- **Half the density** (12 vs 19.3 g/cm3) — 38% lighter for the same volume
- **Higher melting point** (1555 C vs 1064 C) — better for packaging processes

Where palladium alone is not enough — for example, in humid or
chlorine-rich environments — the finish uses **ENEPIG** (Electroless Nickel
Electroless Palladium Immersion Gold): a thin gold layer over the palladium
for corrosion resistance.

**Packaging — 2.5D silicon interposer.**

The six chiplets sit on a silicon interposer, which sits on a carrier PCB.
This is the industry-standard approach: AMD EPYC, Intel Xeon, Apple M-series
all use it. Peripheral I/O (SSD, LAN, power) lives on the carrier PCB, not
inside the module.

---

## 6. Cooling — copper shell + dielectric liquid

Six chiplets plus a central hub produce a lot of heat in a small area.
Air cooling is not enough. HCM-1 uses **single-phase immersion cooling**:

- A **copper shell** encloses the entire module
- Inside, the chiplets are submerged in a **dielectric liquid**
- The liquid circulates, carries heat to the shell, and the shell radiates
  it outward

**Why round, not square.**

The shell is **round**, not square. A square would offer about 27% more
surface area, but the corners create dead zones where the liquid slows
down and heat gets trapped. A round shell lets the dielectric liquid flow
across the surface without obstruction — the same reason cylinders
outperform square rods in heat-exchanger design.

**Why this works:**

- Heat is removed **from every surface at once**, not from one side
- No hot spots — every chiplet sees the same liquid temperature
- The copper shell is both **structural** and **thermal**
- Single-phase (the liquid never boils) is simpler and cheaper than
  two-phase, at some cost in efficiency

This is not speculative — immersion cooling is already deployed at scale in
AI data centres (Microsoft, Google, Intel). HCM-1 brings the same idea down
to a single-module scale.

---

## 7. Open questions

Things that are not resolved. Listed honestly.

- **Thermal budget** — how many watts per chiplet? Never estimated.
- **Power delivery** — voltage and current at the hub? Not specified.
- **Fabrication** — no fab partnership. The interposer and chiplet assembly
  require advanced packaging lines.
- **Software** — how does an OS see six chiplets and one hub? No answer yet.
- **Yield** — even with chiplets, assembly yield on a 6-die module is a
  serious engineering problem.
- **Cost** — no BOM estimate. Advanced packaging is expensive.

These are not failures. They are the boundary of the concept, honestly drawn.
