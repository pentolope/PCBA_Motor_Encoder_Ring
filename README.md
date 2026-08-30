# Circular Multi-Sensor Motor Encoder Ring

A rigid circular PCB that mounts concentrically around a motor shaft and reads rotor position from 12 evenly spaced magnetic or optical sensors.

This repository is the scaffold for **PCBA_Motor_Encoder_Ring**, a rigid circular PCB that mounts concentrically around a motor shaft and measures rotor position using 12 evenly spaced magnetic or optical sensors. The brief pins down the mechanical envelope (outer diameter about 90 mm, central mechanical keep-out diameter at least 40 mm, the central opening/cutout kept free of copper and components as required), the sensing discipline (all sensing elements on a precise common radius, oriented appropriately for the sensing technology), the electrical frame (12 V power input with local regulation, a small MCU collecting the sensors, position reported over CAN or differential serial), and connector placement on the outer perimeter. Everything else — which sensing technology, which parts, the actual sensing radius, whether the centre is a routed cutout or a keep-out region on solid material, the aggregation topology, regulation architecture, stackup, protection strategy, mounting and indexing features — is left to the design agent. No schematic, layout, or part selection exists yet; `docs/architecture.md` is a worksheet of questions the design must answer, not a set of answers.

> **This board has not been designed.** There is no schematic, no layout and no
> part selection here — only the brief, a reading of the brief, and the
> scaffolding a design run needs. That is the intended state of this repository,
> not a gap in it.

## What the brief fixes, and what it leaves open

The brief pins down 16 requirements and deliberately leaves
20 decisions to whoever designs the board. The `Source` column says
which is which: `brief` is quoted from [BRIEF.md](BRIEF.md), `metadata` comes
from the benchmark catalogue, and `open` means the brief does not fix it.

| Aspect | Value | Source |
|---|---|---|
| Board form factor | Rigid circular PCB mounted concentrically around a motor shaft | brief |
| Function | Measures rotor position | brief |
| Outer diameter | About 90 mm | brief |
| Central mechanical keep-out | At least 40 mm diameter | brief |
| Central opening/cutout content | Free of copper and components as required | brief |
| Sensor count and technology family | 12 evenly spaced sensors, magnetic or optical | brief |
| Sensor placement discipline | All sensing elements on a precise common radius, with orientations appropriate to the sensing technology | brief |
| Controller | A small MCU that collects the sensors | brief |
| Host reporting interface | CAN or differential serial | brief |
| Power input | 12 V, with local regulation on the board | brief |
| Connector placement | On the outer perimeter | brief |
| Likely layer count | 4 | metadata |
| Benchmark classification | Category mechanical-constrained-sensor; difficulty 4/5; brief detail 4/5; primary stressors: annular board geometry, repeated sensor placement, radial routing, connector/keepout | metadata |
| Sensing technology (magnetic vs optical), sensor part, actual sensing radius, and the physical form of the central opening | Not fixed by the brief — design agent's choice, to be made and documented | open |

The full split, with the verbatim brief text substantiating every fixed
requirement, is in [board/requirements.md](board/requirements.md) and
machine-readably in [board/requirements.json](board/requirements.json).

**Missing details are design freedom, not permission to fabricate unstated user
requirements.** A choice the brief left open is recorded as a decision, with its
reasoning — never promoted into a requirement.

## Benchmark position

| | |
|---|---|
| Benchmark id | 30 of 32 |
| Category | mechanical-constrained-sensor |
| Difficulty | 4 / 5 |
| Brief detail | 4 / 5 |
| Likely layer count | 4 |
| Primary stressors | annular board geometry, repeated sensor placement, radial routing, connector/keepout |

This is the benchmark's mechanical-constrained-sensor case at difficulty 4/5 with a detail-4 brief: the geometry is stated in numbers — outer diameter about 90 mm, central mechanical keep-out diameter at least 40 mm — so the test is whether an agent honours a stated circular envelope with a large central keep-out rather than defaulting to a rectangular board. The metadata's stressors — annular board geometry, repeated sensor placement, radial routing, connector/keepout — point at whether 12 identical sensor sites land on a genuinely common radius at genuinely even angles, whether routing across a ring whose centre must stay free of copper stays symmetric, and whether the perimeter connectors and the central opening/cutout are treated as real constraints rather than annotations. The brief deliberately leaves the sensing technology, every part, the sensing radius itself, and the physical form the central opening takes open, so it also tests whether an agent chooses and documents rather than silently assuming.

This repository is one of thirty-two. The suite, the protocol and the results
live in [PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench).

## Repository layout

| Path | Contents |
|---|---|
| `BRIEF.md` | the supplied brief — authoritative, preserved byte for byte, never edited |
| `board/requirements.md` | what the brief fixes, what it leaves open, and where decisions get recorded |
| `board/requirements.json` | the same split, machine-readable, each fixed requirement bound to brief text |
| `board/manifest.template.json` | the toolkit's minimum manifest, pre-filled for this board |
| `board/toolchain.json` | where this board's build finds KiCad and the router |
| `benchmark/metadata.json` | the supplied catalogue entry — category, difficulty, detail, stressors |
| `docs/architecture.md` | the decisions this board must make, as questions, unanswered |
| `docs/sources.md` | the classes of evidence the design will have to cite |
| `docs/status.md` | what exists, what does not, and what is deliberately absent |
| `candidates/` | disposable search output, ignored by Git |
| `tooling/PCBA_AutoDesignAndTest` | the shared verification/routing/release toolkit, as a pinned submodule |

## Getting the repository

The toolkit is a submodule and carries KiCad Routing Tools as a submodule of its
own, so clone recursively:

```bash
git clone --recursive https://github.com/pentolope/PCBA_Motor_Encoder_Ring.git
```

```bash
git submodule update --init --recursive
```

## Designing the board

Generic verification, routing and release logic is **not** written here. It is
consumed from `tooling/PCBA_AutoDesignAndTest`, which is board-agnostic by
construction and must stay that way; this repository owns the board and nothing
else. Start from
[the toolkit's onboarding guide](tooling/PCBA_AutoDesignAndTest/examples/onboarding.md),
and see [CLAUDE.md](CLAUDE.md) for the rules a design run works under.

```bash
python3 tooling/PCBA_AutoDesignAndTest/run.py preflight
```

## Brief integrity

`BRIEF.md` SHA-256 `f2bc0fba6dc9f83993ead30b7bdda4e1034551b5fb0a8ccf2aa5fcfb551fb1da`

Every quotation in `board/requirements.json` is bound to those exact bytes. If
the brief ever changes, the bindings are stale by construction — which is the
point of recording the digest.
