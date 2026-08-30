# Architecture — Circular Multi-Sensor Motor Encoder Ring

**A worksheet, not a design.** Every line below is a question this board has to
answer, and none of them is answered here. Nothing in this file is a
recommendation, and the order of the sections carries no preference.

The questions were derived from [the brief](../BRIEF.md) and from what this
board is meant to stress in the benchmark:

- annular board geometry
- repeated sensor placement
- radial routing
- connector/keepout

Those are the places where a wrong answer shows up in copper.

Answer them in this file as the design is made, each answer carrying the
evidence that supports it, and record the corresponding choice against its
`OPEN-nn` entry in [board/requirements.md](../board/requirements.md). An answer
without evidence is a guess wearing a document's clothes — and this benchmark is
allowed to refuse an unsupported claim rather than invent one.

## Sensing technology and the rotor-side interface

- Magnetic or optical — which is chosen, and what in this application decides it?
- What target does the sensor see (magnet ring, code wheel, shaft feature), and who supplies it?
- What air gap does the chosen sensor need, and does the mounting scheme hold it across 12 sites?
- What sensor output type (analog, digital, incremental, absolute) is assumed, and what does that imply for the MCU?
- How does the sensing technology constrain the rotational orientation of each sensing element, per the brief's 'orientations appropriate to the sensing technology'?
- How is the motor's proximity (stray field, optical contamination, heat) handled for the chosen technology?

## Annular envelope and mechanical constraints

- What outer diameter is used, and how does 'about 90 mm' get converted into a toleranced dimension?
- What inner diameter is used, and by how much does it exceed the 40 mm minimum keep-out — and why?
- Is the centre a routed cutout or a keep-out region on solid material, and what does the fabricator require for that feature?
- What radial width of usable annulus remains after keep-out, edge clearance, and connector footprints are subtracted?
- What mounting holes, standoffs and fasteners fix the ring concentrically, and what pattern do they use?
- Is there an angular indexing or keying feature that registers the ring's zero to the motor, and where does it sit?
- Which face is the sensing face, and is the opposite face available for placement?

## Sensor ring placement and precision

- What is the sensing radius, and what tolerance is placed on it?
- What angular positions do the 12 sites occupy, and what angular tolerance is claimed?
- What is the placement error budget: fabrication feature-to-copper registration, assembly placement accuracy, assembly rotational accuracy, and part-internal die-to-package offset — and do they sum within the claimed 'precise common radius'?
- How are the 12 sensor sites positioned — from one shared geometric definition, or site by site — and what does that choice cost in accuracy and in maintainability?
- How is the actual as-designed placement extracted and checked against the intended polar coordinates?
- Are all 12 sites identical, including local decoupling and orientation, or does anything break the symmetry?

## Radial routing and symmetry

- What does 'symmetric routing' mean concretely here — matched lengths, matched layer sequence, matched via count, or matched neighbourhood?
- Which quantity is actually matched across the 12 channels, and to what tolerance?
- Do the sensor channels route radially inward toward a central hub region, or circumferentially around the ring, and what does that cost?
- Where does the MCU sit so that the 12 channel routes can be made comparable?
- How are inevitable asymmetries near the connector sector accounted for?
- How is the routing across the 12 channels produced relative to the placement, and what would a change to the sensing radius do to the routing symmetry?

## MCU and sensor aggregation

- How many sensor signals must arrive at the MCU, and what does that imply for pin count and peripheral count?
- Is aggregation point-to-point, bussed, multiplexed, or daisy-chained — and how does that choice interact with the routing symmetry requirement?
- If a shared bus is used, how are 12 identical devices addressed or selected?
- What sample-simultaneity does position measurement need across the 12 channels, and can the chosen scheme deliver it?
- What resolution and update rate does the MCU need to sustain to report position?
- What programming/debug access exists, and where does it physically go on a ring with a full central keep-out?

## Host interface: CAN or differential serial

- Which interface is implemented — CAN, differential serial, or both — and what makes that the right answer here?
- Which transceiver class is used, at what supply, and with what common-mode and fault requirements?
- Does this node carry bus termination, and is that fixed or selectable?
- How are data and power split across the perimeter connector(s)?
- What message format, rate and node addressing are exposed to the host?
- What protection does the bus need at the connector, given a cable running near a motor?

## 12 V input and local regulation

- What rails does the board need, at what currents, and what is the total budget across 12 sensors plus MCU plus the host-link devices?
- Is regulation linear or switching, and how is that justified against the 12 V drop and available annular area?
- If switching, where does the switching node sit relative to the sensing elements, and how is its field kept out of them?
- How is the sensor supply decoupled or separated from the digital and host-link supply?
- What thermal path exists for the regulator in a narrow annulus?
- What does the input see on a 12 V motor-adjacent supply — reverse polarity, transients, brownout — and what is done about each?

## Connectors and perimeter keep-outs

- How many connectors are on the perimeter, and what does each carry?
- What angular sector do they occupy, and does that sector collide with any of the 12 sensor sites?
- What mating clearance envelope does each connector need beyond its footprint, and is that reserved as a keep-out?
- Does cable exit direction conflict with the motor housing or with the concentric mount?
- Is the perimeter sector occupied by connectors the reason for any asymmetry in the routing, and is that documented?

## Stackup, grounding and return paths

- What layer count is used, and does it match the benchmark's likely-4 expectation or deviate with a stated reason?
- With the central opening/cutout kept free of copper as required, what is the actual return path under each radial sensor trace?
- Is the ground an unbroken annulus, and where are the unavoidable slots or splits?
- Are sensor analog returns and power/digital returns partitioned, and if so where do they meet?
- How much of the annulus is consumed by the power rails, and does that leave enough contiguous plane for return?
- How is the plane structure verified rather than asserted?

## Manufacturability of a ring board

- What fabricator capability class is targeted, and what are its minimum trace/space, minimum hole, and internal-cutout rules?
- What positional tolerance does the fabricator hold between the routed inner/outer edges and the copper features — and does the sensing-radius claim survive it?
- What placement positional and rotational accuracy does the assembler hold, and is that consistent with the sensor orientation requirement?
- Does the ring need a panel, tabs, or a carrier to be assembled, and where do break tabs land relative to keep-outs?
- Are there fiducials, and are they placed so that the 12 repeated sites are accurately registered?
- What is the panel utilisation cost of a 90 mm annulus, and is it acceptable?

## Bring-up, calibration and test

- How is each of the 12 channels exercised and verified independently?
- How is the as-built sensing radius and angular spacing actually measured rather than assumed?
- Is there a calibration step that establishes angular zero, and where is the calibration stored?
- What test points or connector-accessible signals exist, given the perimeter-only connector constraint and the central keep-out?
- What does a pass/fail criterion for 'position reporting works' look like on the bench, without a motor attached?
- How are failures localised to a specific sensor site among 12 identical ones?

## Repository and toolkit boundary

- Which parts of the ring geometry and placement logic belong in this repo versus the shared toolkit?
- How is the ring geometry expressed in this repo, and what has to happen to placement and routing if the sensing radius changes?
- What generated search/simulation data is disposable, and what is explicitly promoted?
- What is the minimum set of configuration files this board needs to consume the shared toolkit unchanged?

## Answers still owed

All of them. See [status.md](status.md).
