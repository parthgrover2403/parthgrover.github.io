# Design and Compensation of a 1.5V CMOS Low Dropout (LDO) Voltage Regulator

## Problem Statement
Designed a transistor-level 1.5V Low Dropout (LDO) voltage regulator in LTspice for a power management course final project. The objective was to maintain a regulated 1.5V output across varying load conditions while satisfying multiple analog performance constraints. The project required complete small-signal and transient simulation verification. The primary design challenge involved balancing transient response, loop stability, and low standby power while maintaining regulation across a wide load current range.

Picture here for the LDO

## Design Specifications

| Parameter | Target |
|--------|--------|
| Output Voltage | 1.5 V |
| Maxiumum Load Current | 100 mA |
| Load Transient Range | 1 mA → 50 mA |
| Maximum Output Voltage Peaking | ≤ 100mV |
| Load Regulation | < 1% |
| Output Load Capacitance (CL) | 100 pF |
| Standby Power Consumption | < 5 mW |
| Phase Margin (PM) | > 45 deg |

---

## Architecture & Circuit Design

The LDO architecture was implemented using three primary blocks: a two-stage error amplifier, a PMOS pass transistor, and a resistive feedback network. The error amplifier consisted of stacked current mirror stages with differential input pairs to compare the 1V reference voltage against the feedback voltage derived from the output node. A PMOS pass device was selected as the regulating transistor to support low-dropout operation while sourcing up to 100mA load current. The pass transistor was sized analytically using long-channel MOSFET current equations and finalized at approximately 7.11mm/0.4µm (W/L) to satisfy the required current drive capability and transient response targets.

To achieve the target output voltage of 1.5V, a resistor divider network consisting of 300kΩ and 600kΩ resistors was designed according to the standard feedback relation:

Vout = Vref(1+Rf1/Rf2)

Loop stability was improved through frequency compensation techniques. Initial loop gain simulations revealed an unstable phase margin at light-load conditions, motivating the addition of compensation zeros using both output capacitor ESR and Miller compensation. A 300pF Miller capacitor and 50Ω series resistor were introduced between the amplifier output and pass transistor stage to improve phase margin and suppress oscillatory transient behavior. Compensation was intentionally designed around worst-case light-load conditions, where the reduced transconductance of the pass device created the most challenging stability scenario.
<p align="center">
  <img src="../assets/opamp/schematic.png" width="500">
</p>
<p align="center"><em>Figure 1: Top-level schematic of the two-stage operational amplifier.</em></p>

<p align="center">
  <img src="../assets/opamp/cmfb.png" width="500">
</p>
<p align="center"><em>Figure 2: Common-mode feedback (CMFB) circuit used to regulate output common-mode level.</em></p>

---

## Compensation & Stability

- Miller compensation capacitor used between the first and second stages
- Triode-region transistor employed as a nulling element for pole-zero placement
- Compensation designed to remain stable across PVT variations
- Both differential-mode and CMFB loops independently verified for stability

<p align="center">
  <img src="../assets/opamp/open.png" width="500">
</p>
<p align="center"><em>Figure 3: Open-loop simulation testbench configuration.</em></p>

<p align="center">
  <img src="../assets/opamp/closed.png" width="500">
</p>
<p align="center"><em>Figure 4: Closed-loop simulation testbench configuration.</em></p>

---

## Simulation & Verification

<p align="center">
  <img src="../assets/opamp/gain.png" width="500">
</p>
<p align="center"><em>Figure 5: Post-layout AC response showing DC gain.</em></p>

<p align="center">
  <img src="../assets/opamp/slew_rate.png" width="500">
</p>
<p align="center"><em>Figure 6: Transient simulation demonstrating slew rate performance.</em></p>

<p align="center">
  <img src="../assets/opamp/noise.png" width="500">
</p>
<p align="center"><em>Figure 7: Input-referred noise integrated from 1 Hz to 100 MHz.</em></p>

<p align="center">
  <img src="../assets/opamp/im3.png" width="500">
</p>
<p align="center"><em>Figure 8: IM3 distortion analysis using a 1 Vpp, 1 MHz two-tone input.</em></p>

---

## Layout & Post-Layout Results

<p align="center">
  <img src="../assets/opamp/layout.png" width="500">
</p>
<p align="center"><em>Figure 9: Final chip layout including pads, op-amp core, and CMFB circuitry.</em></p>

### Post-Layout Performance Summary

| Metric | Achieved |
|------|---------|
| DC Gain | 64.03 dB |
| Power Dissipation | 1.298 mW |
| GBW | 139 MHz |
| Slew Rate | 89.98 V/µs |
| Input-Referred Noise | 13.37 µV RMS |
| IM3 | −59.8 dB |
| Differential Phase Margin | 63° |
| CMFB Phase Margin | 68.25° |

All specifications were met after parasitic extraction.

---

## Key Learnings
- Tradeoffs between gain, bandwidth, and power in multi-stage amplifiers
- Importance of compensation strategy for closed-loop stability
- Impact of parasitic extraction on analog performance
- Noise-aware input stage selection and biasing

