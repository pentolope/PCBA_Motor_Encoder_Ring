# PCBA_Motor_Encoder_Ring — Circular Multi-Sensor Motor Encoder Ring
## Design brief

Design a rigid circular PCB that mounts concentrically around a motor shaft and measures rotor position using 12 evenly spaced magnetic or optical sensors. Outer diameter about 90 mm; central mechanical keep-out diameter at least 40 mm. All sensing elements must be positioned on a precise common radius with orientations appropriate to the sensing technology. A small MCU collects the sensors and reports position over CAN or differential serial. Power input is 12 V with local regulation. Place connectors on the outer perimeter and keep the central opening/cutout free of copper and components as required. The repeated radial geometry should make placement constraints and symmetric routing important.

## Functional requirements

- A maximum shaft speed, update rate and total angular error budget shall be defined before layout; the tolerances below allocate from it.
- The 12 channels shall be sampled simultaneously, or with a fixed known skew that firmware corrects to one instant.
- Sensor-to-channel mapping shall be fixed by layout, post-reset behaviour stated, and per-channel faults reported distinguishably from valid position.

## Ring geometry and placement

- Circular outline of about 90 mm; any deviation shall follow the mounting interface, not routing convenience.
- The concentric keep-out of at least 40 mm diameter shall hold no components, no copper on any layer, and no vias.
- A datum shall hold the sensing circle concentric with the shaft and the 12 elements in one axial plane; fiducials shall make a 30°-rotated placement impossible.

## Sensor channels and matching

- Each element's rotation shall give its sensitive axis or aperture an identical relationship to the local radial and tangential directions.
- Per-instance rotation and radial and tangential placement tolerance shall be released assembly data, tight enough for the error budget.
- Channel front ends and filtering shall be identical, so gain and delay mismatch come only from part tolerance.
- If magnetic, ferromagnetic parts and switching conductors shall be excluded near the sensing radius; if optical, apertures shall be defined and adjacent-channel light blocked.

## Power and rails

- 12 V shall be the only input; all other rails shall be generated on board and sized for 12 active channels, MCU and transceiver at worst case.
- Sensor-rail noise shall stay inside the budget with no ripple aliasing into the sample rate, and IR drop to each element equal within tolerance.
- The input shall carry reverse-polarity protection, transient clamping, a fuse or current limit, and bulk capacitance for harness inductance.

## Interfaces and connectors

- Connectors shall sit on the outer perimeter clear of the keep-out, mate with the board installed, and route cable away from the rotor.
- The link pair shall meet the chosen standard's impedance, matching and stub rules, cross no plane split, and carry harness-grade transient protection.
- Termination shall be an explicit fitted option, and connectors keyed and pinned so a mis-mate cannot put 12 V on a signal pin.

## Symmetric routing and noise immunity

- Under a 30° rotation, each channel's trace length, layer sequence, via count, reference plane and neighbour spacing shall map onto the next channel's.
- Every sensor signal shall run over a continuous reference; the keep-out boundary shall not force a plane-discontinuity crossing.
- Regulator, transceiver and clock returns shall stay out of the sensing annulus, and any residual coupling shall be equal at all 12 positions.

## Test, bring-up and calibration

- Test points shall exist for the input, every local rail and each of the 12 sensor signals, reachable outside the keep-out.
- MCU programming and debug access shall sit outside the keep-out and be usable without removing components.
- A diagnostic mode shall stream per-channel raw values, and calibration constants shall be stored on board and readable over the link.

## Open choices

- Sensing technology, magnetic or optical: it sets the orientation rule, exclusion zones, masking, and whether the centre must be a true opening.
- Whether the centre is a physical cut-out or an unpopulated copper-free region, and whether position is absolute or incremental.
- MCU and link (CAN or differential serial), judged on 12-channel throughput within the skew limit, calibration storage, bit rate and isolation.
- Regulation topology, layer count and stack-up, mounting pattern and connector family, each following from the constraints above.
