# Sources — Circular Multi-Sensor Motor Encoder Ring

The evidence this board's design will have to cite. **Classes of document, not
documents:** the specific parts are not chosen yet, so naming a datasheet here
would be choosing one.

A number that reaches the board carries its provenance: source, document id or
URL, retrieval date, units, and the condition it applies under. A number without
that is not evidence, and no live network lookup may change a validation or
release result.

| Kind of source | What the design needs from it |
|---|---|
| Position-sensor datasheets (magnetic or optical, per the chosen technology) | Establishes sensing axis and required package orientation, air-gap range, target magnet or code-wheel requirements, supply and output interface — all of which the brief's 'orientations appropriate to the sensing technology' requirement depends on. |
| MCU datasheet and reference manual | Needed to show the chosen 'small MCU' actually has the pin count, peripheral instances and sampling capability to collect 12 sensor channels at the intended rate, in a package that fits the annulus. |
| Communications transceiver datasheets for the link chosen (CAN, or the differential-serial PHY selected) | Supply rail, common-mode range, fault and ESD ratings, and termination requirements for the reporting link the brief requires over CAN or differential serial. |
| Bus physical-layer standard for the chosen link | Topology, termination, stub-length and node-count rules that determine whether a single perimeter connector node is legal on the intended bus. |
| Regulator datasheets and layout application notes for the regulation topology chosen | Input range, efficiency and thermal derating for converting the brief's 12 V input locally, plus the layout guidance needed to argue the switching or dissipating element does not corrupt 12 nearby sensing sites. |
| PCB fabricator capability and tolerance documents | Minimum trace/space and hole size for the chosen layer count, internal cutout/routing capability, and — critically — edge-to-copper positional tolerance, which bounds how 'precise' the common sensing radius can honestly be claimed to be. |
| Assembly-house process capability documentation | Component placement positional and rotational accuracy, which is the second half of the tolerance stack behind the common-radius and sensor-orientation requirements. |
| Motor and rotor mechanical interface drawings or stated interface assumptions | Shaft, hub and housing dimensions that justify the ~90 mm outer diameter and the ≥40 mm central mechanical keep-out, and the axial clearance that sets the sensing air gap. |
| Connector manufacturer datasheets and mating/keep-out drawings | Perimeter footprint plus the mating clearance envelope and cable exit direction, needed to prove the connectors fit the outer perimeter without intruding on sensor sites. |
| ESD, EMC and transient-immunity standards applicable to 12 V cable-connected equipment | Defines what the input and bus protection must survive, so protection is sized against a stated level rather than asserted. |
| Magnet or encoder-target supplier data (if magnetic sensing is chosen) | Pole count, field strength versus gap, and mechanical tolerance of the rotor-side target, which set the achievable resolution and the required sensing radius. |
| Shared PCBA_AutoDesignAndTest toolkit documentation | Defines how placement, keep-outs and design rules are expressed for this repo, so ring-specific geometry stays in the board repo as the brief's benchmark intent requires. |

## Recording a source, once one is chosen

Replace the class with the actual document — manufacturer, part number, revision
and date — and state the fact taken from it, in the units the document uses.
Keep the class row: it says why the document was needed.

JLCPCB-wide process limits are **not** recorded here. They live in the toolkit's
`profiles/jlcpcb/`, with their own provenance; this board records only its own
tighter targets and its own selected options. A limit copied into two places is
a rival threshold, and the toolkit has a gate that says so.
