# Benchmark entry — board 30 of 32

[metadata.json](metadata.json) is the supplied catalogue entry for this board,
preserved byte for byte from the seed pack. It is the same record that appears
in `boards_index.json` in
[PCBA_AutoDesignAndTest_Bench](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench), and the two must agree.

| | |
|---|---|
| Repository | `PCBA_Motor_Encoder_Ring` |
| Board id | `motor_encoder_ring` |
| Category | mechanical-constrained-sensor |
| Difficulty | 4 / 5 |
| Brief detail | 4 / 5 |
| Likely layer count | 4 |
| Primary stressors | annular board geometry, repeated sensor placement, radial routing, connector/keepout |

`difficulty` is how hard the board is. `detail` is how much of it the brief
states — and a low `detail` is not a low bar. A detail-1 brief leaves the
architecture open on purpose, and an agent that fills the silence with invented
user requirements has failed the board more thoroughly than one that designs it
badly.

This is the benchmark's mechanical-constrained-sensor case at difficulty 4/5 with a detail-4 brief: the geometry is stated in numbers — outer diameter about 90 mm, central mechanical keep-out diameter at least 40 mm — so the test is whether an agent honours a stated circular envelope with a large central keep-out rather than defaulting to a rectangular board. The metadata's stressors — annular board geometry, repeated sensor placement, radial routing, connector/keepout — point at whether 12 identical sensor sites land on a genuinely common radius at genuinely even angles, whether routing across a ring whose centre must stay free of copper stays symmetric, and whether the perimeter connectors and the central opening/cutout are treated as real constraints rather than annotations. The brief deliberately leaves the sensing technology, every part, the sensing radius itself, and the physical form the central opening takes open, so it also tests whether an agent chooses and documents rather than silently assuming.

## What goes here

Compact results only: metrics, verdicts, and the commit each was measured at.
The evidence for a result is the artefact the toolkit recomputes, not a summary
of it.

Routing search output, candidate pools, build trees and field-solver dumps do
**not** go here. They are ignored by [.gitignore](../.gitignore) and are
regenerated from what is committed. Thirty-two repositories share one benchmark
clone; weight here is paid thirty-two times.

## Protocol

The attempt protocol is defined once, in the umbrella repository, so that
thirty-two boards cannot drift into thirty-two protocols. See
[PCBA_AutoDesignAndTest_Bench/BENCHMARK.md](https://github.com/pentolope/PCBA_AutoDesignAndTest_Bench/blob/main/BENCHMARK.md).
