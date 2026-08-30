# Requirements — Circular Multi-Sensor Motor Encoder Ring

Two lists. The difference between them is the whole point of this file.

A **fixed requirement** is something [BRIEF.md](../BRIEF.md) asks for. Each one
below quotes the brief text that substantiates it; if a statement cannot be
quoted, it is not a requirement here. An **open decision** is a choice the brief
deliberately left to whoever designs this board.

> Missing details are design freedom, not permission to fabricate unstated user
> requirements.

Promoting a decision into a requirement is the failure this file exists to
prevent. Record a choice under the decision it answers, with the reasoning that
made it — never by adding it to the list above.

Bound to `BRIEF.md` SHA-256 `f2bc0fba6dc9f83993ead30b7bdda4e1034551b5fb0a8ccf2aa5fcfb551fb1da`.

## Fixed by the brief

### REQ-01 — The board is a rigid circular PCB that mounts concentrically around a motor shaft.

Brief text:

> Design a rigid circular PCB that mounts concentrically around a motor shaft

### REQ-02 — The board measures rotor position.

Brief text:

> measures rotor position using 12 evenly spaced magnetic or optical sensors.

### REQ-03 — Sensing uses exactly 12 evenly spaced sensors, of either magnetic or optical technology.

Brief text:

> measures rotor position using 12 evenly spaced magnetic or optical sensors.

### REQ-04 — Outer diameter is about 90 mm.

Brief text:

> Outer diameter about 90 mm; central mechanical keep-out diameter at least 40 mm.

### REQ-05 — A central mechanical keep-out of at least 40 mm diameter is preserved.

Brief text:

> Outer diameter about 90 mm; central mechanical keep-out diameter at least 40 mm.

### REQ-06 — All sensing elements are positioned on a precise common radius.

Brief text:

> All sensing elements must be positioned on a precise common radius with orientations appropriate to the sensing technology.

### REQ-07 — Sensing element orientations must be appropriate to the chosen sensing technology (i.e. rotational orientation of each site is a design output, not arbitrary).

Brief text:

> All sensing elements must be positioned on a precise common radius with orientations appropriate to the sensing technology.

### REQ-08 — A small MCU on the board collects the sensors.

Brief text:

> A small MCU collects the sensors and reports position over CAN or differential serial.

### REQ-09 — The MCU reports position over CAN or over differential serial.

Brief text:

> A small MCU collects the sensors and reports position over CAN or differential serial.

### REQ-10 — Power input to the board is 12 V.

Brief text:

> Power input is 12 V with local regulation.

### REQ-11 — Regulation from the 12 V input to whatever rails the board needs is done locally on the board.

Brief text:

> Power input is 12 V with local regulation.

### REQ-12 — Connectors are placed on the outer perimeter of the ring.

Brief text:

> Place connectors on the outer perimeter and keep the central opening/cutout free of copper and components as required.

### REQ-13 — The central opening/cutout is kept free of copper and components as required.

Brief text:

> Place connectors on the outer perimeter and keep the central opening/cutout free of copper and components as required.

### REQ-14 — The repeated radial geometry is treated as load-bearing: placement constraints between the 12 sensor sites and symmetry of the routing are first-class design requirements, not incidental outcomes.

Brief text:

> The repeated radial geometry should make placement constraints and symmetric routing important.

### REQ-15 — Where the brief leaves a choice open, the design agent makes and documents a reasonable engineering decision rather than inventing hidden user requirements; stated requirements are authoritative.

Brief text:

> Treat stated requirements as authoritative; where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements.

### REQ-16 — This repository stays a consumer of the shared PCBA_AutoDesignAndTest toolkit; board-specific logic does not accumulate in the toolkit.

Brief text:

> The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.

## Open — the design agent decides

### OPEN-01 — Whether the sensing technology is magnetic or optical.

The brief offers the two as an explicit either/or ("magnetic or optical sensors") and does not pick one; the choice drives sensor orientation, the rotor-side target, and the whole placement geometry.

*Decision:* **not yet made.**

### OPEN-02 — Which specific sensor device is used — package, output type (analog, digital, incremental, absolute), interface, and supply rail.

The brief names no part, vendor, or interface for the sensing elements; it fixes only their number, spacing, radius discipline and technology family.

*Decision:* **not yet made.**

### OPEN-03 — The actual sensing radius (and therefore the sensor pitch circle diameter).

The brief requires a "precise common radius" and bounds the annulus with an ~90 mm outer diameter and a ≥40 mm central keep-out, but never states the radius itself.

*Decision:* **not yet made.**

### OPEN-04 — MCU selection: family, core, package, pin count, clocking, and how many sensor channels it must terminate directly.

The brief says only "a small MCU" and names no device, architecture, or vendor.

*Decision:* **not yet made.**

### OPEN-05 — Which host link is implemented — CAN or differential serial (or both) — and which transceiver/PHY realises it.

The brief gives the two as alternatives and names no transceiver, connector, data rate, or protocol layer.

*Decision:* **not yet made.**

### OPEN-06 — Sensor aggregation topology: point-to-point to the MCU, a shared bus, multiplexing, daisy-chaining, or a mixture.

The brief states only that the MCU "collects the sensors"; it is silent on how the 12 channels reach it, which is the decision that determines whether radial routing can stay symmetric.

*Decision:* **not yet made.**

### OPEN-07 — Power architecture below the 12 V input: linear vs switching, number and value of rails, sequencing, and how sensor supplies are decoupled or separated from digital supplies.

The brief fixes the input voltage and that regulation is local, and nothing else about topology, rail voltages, or current budget.

*Decision:* **not yet made.**

### OPEN-08 — Connector selection: how many connectors, type, pin count, orientation, mating direction, and retention.

The brief fixes only that connectors sit on the outer perimeter; no part, pin count, or cable interface is named.

*Decision:* **not yet made.**

### OPEN-09 — Protection strategy for the 12 V input and the communications bus — reverse polarity, overvoltage/transient, overcurrent, and ESD.

The brief is silent on protection entirely; the motor-adjacent, 12 V, cable-connected context is a stressor to be addressed, not a specified circuit.

*Decision:* **not yet made.**

### OPEN-10 — Stackup: final layer count, copper weights, dielectric materials, finished thickness, and surface finish.

The brief states no stackup; the metadata's "likely layer count: 4" is a benchmark expectation, not a stated user requirement.

*Decision:* **not yet made.**

### OPEN-11 — Exact annulus geometry: the inner diameter actually used above the 40 mm minimum, whether the centre is a true routed cutout or a keep-out on solid board, and edge/cutout tolerance callouts.

The brief gives a minimum keep-out diameter and refers to a "central opening/cutout" without fixing which form it takes or how tightly it is toleranced.

*Decision:* **not yet made.**

### OPEN-12 — Mechanical mounting: number, size and bolt-circle of mounting holes, fastener and standoff scheme, and any angular indexing/keying feature that registers the ring to the motor.

The brief says the board mounts concentrically around the shaft but specifies no mounting hardware, hole pattern, or angular registration feature.

*Decision:* **not yet made.**

### OPEN-13 — Assembly sidedness: single- or double-sided placement, and which side faces the rotor target.

The brief does not state which face of the ring is the sensing face or whether the back side may carry parts.

*Decision:* **not yet made.**

### OPEN-14 — How an angular zero/index is established — whether any index mark, reference sensor, or startup calibration exists.

The brief requires position reporting from 12 evenly spaced sensors but says nothing about absolute reference, homing, or index.

*Decision:* **not yet made.**

### OPEN-15 — The rotor-side interface: target magnet ring, code wheel or equivalent, its pole/line count, and the target air gap.

The brief describes only the PCB side of the system; the moving target and the mechanical gap it presents are not specified.

*Decision:* **not yet made.**

### OPEN-16 — Position resolution, update rate, latency, and the on-wire message format and node addressing over the chosen link.

The brief names the transport as CAN or differential serial but fixes no performance figure, protocol, framing, or address scheme.

*Decision:* **not yet made.**

### OPEN-17 — Grounding and return strategy for a ring whose centre must stay free of copper — how continuous return paths are maintained under 12 sets of radial traces, and whether sensor and power returns are partitioned.

The brief is silent on grounding; it only requires the central opening/cutout to be kept free of copper as required, which is what makes the return path a genuine design problem.

*Decision:* **not yet made.**

### OPEN-18 — Bus electrical details: whether this node carries termination, whether it is bus-powered or separately powered, and stub/branch handling on the perimeter connectors.

The brief mentions CAN or differential serial and a 12 V input but does not say how the node sits on the bus or whether power and data share a connector.

*Decision:* **not yet made.**

### OPEN-19 — Environmental and operating envelope: temperature range, vibration, ingress, and the magnetic/EMI environment near the motor.

The brief states no environmental conditions, ratings, or qualification requirements.

*Decision:* **not yet made.**

### OPEN-20 — Fabrication and assembly vendor and the process capability class targeted (minimum trace/space, minimum hole, internal cutout routing, placement positional and rotational accuracy).

The brief names no fabricator, process, or tolerance class, yet the "precise common radius" requirement can only be defended against a specific stated capability.

*Decision:* **not yet made.**

## Where a decision gets recorded

1. Answer it under its `OPEN-nn` heading above, with the reasoning and the
   evidence that made the choice.
2. Set `chosen` and `rationale` on the matching entry in
   [requirements.json](requirements.json).
3. Cite the datasheet or standard in [docs/sources.md](../docs/sources.md).

A choice recorded this way stays visibly a choice. That is what lets a later
reader tell this board's engineering apart from its brief.

## Where this board is most likely to be faked

Places where a design run would be tempted to assert something it cannot
substantiate:

- The 'precise common radius' claim is the single easiest thing to fake. A design can assert that 12 sensors sit on a common radius without ever publishing the polar coordinate table, the achieved angular error, or a tolerance stack combining fabricator edge-to-copper registration with assembler placement and rotational accuracy. The claim is only real if it is computed and bounded.
- The brief gives 'magnetic or optical' as an open either/or, and its benchmark-intent paragraph asks that open choices be made and documented rather than left implicit. A design that never states which technology it assumed, or that silently mixes assumptions belonging to the two, leaves every downstream geometry claim uncheckable. Accommodating both is a legitimate answer if it is stated as a deliberate choice and its cost in area and parts is carried.
- Sensor orientation is a stated requirement, not decoration. Placing 12 parts at even angles with identical rotation (or with rotation nobody checked against the sensing axis) is a common way to satisfy the geometry while violating 'orientations appropriate to the sensing technology'.
- The usable annulus between a ≥40 mm keep-out and an ~90 mm outer diameter is narrow. Claiming that 12 sensor sites, an MCU, local 12 V regulation, whatever realises the host link, and perimeter connectors all fit is worthless without an explicit area budget; the temptation is to declare it fits and move on.
- 'Symmetric routing' invites an aesthetic assertion. Symmetry must be reduced to a measurable — what is matched, across which 12 channels, to what tolerance — and the asymmetry forced by the connector sector must be named rather than hidden.
- Ground continuity around a ring whose central opening/cutout must be kept free of copper is a real problem. 'Solid ground plane' is easy to write and hard to have; the return path under each radial trace needs to be shown, not claimed.
- The brief specifies no target magnet, code wheel, pole count, air gap, resolution or update rate. Inventing these to make the sensing arithmetic close is the most likely fabrication on this board — they belong in open decisions with a stated, justified assumption, not in the requirements.
- The metadata's 'likely layer count: 4' is benchmark guidance, not a user requirement. Presenting it as a fixed constraint, or exceeding it without acknowledging the cost, both misrepresent the source material.
