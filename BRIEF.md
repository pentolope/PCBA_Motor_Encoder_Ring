# PCBA_Motor_Encoder_Ring — Circular Multi-Sensor Motor Encoder Ring

**Benchmark ID:** 30  
**Difficulty:** 4/5  
**Brief detail:** 4/5  
**Category:** mechanical-constrained-sensor  
**Likely layer count:** 4  
**Primary stressors:** annular board geometry, repeated sensor placement, radial routing, connector/keepout

## Design brief

Design a rigid circular PCB that mounts concentrically around a motor shaft and measures rotor position using 12 evenly spaced magnetic or optical sensors. Outer diameter about 90 mm; central mechanical keep-out diameter at least 40 mm. All sensing elements must be positioned on a precise common radius with orientations appropriate to the sensing technology. A small MCU collects the sensors and reports position over CAN or differential serial. Power input is 12 V with local regulation. Place connectors on the outer perimeter and keep the central opening/cutout free of copper and components as required. The repeated radial geometry should make placement constraints and symmetric routing important.

## Benchmark intent

This brief is intentionally one member of a heterogeneous PCBA-autodesign benchmark. Treat stated requirements as authoritative; where the brief leaves choices open, make and document reasonable engineering decisions rather than inventing hidden user requirements. The repository should remain a consumer of the shared `PCBA_AutoDesignAndTest` toolkit rather than accumulating board-specific logic in the toolkit.
