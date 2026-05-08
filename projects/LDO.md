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
| Supply Voltage (VDD) | 2 V |

---

## Architecture and Design Approach

The LDO was divided into three major functional blocks:

- Two-stage error amplifier
- PMOS pass transistor
- Resistive feedback network

The error amplifier utilized stacked current mirror stages with differential inputs to compare the feedback voltage against a 1V reference source. The PMOS pass device regulated current delivery to the output node while supporting low-dropout operation.

The output voltage was determined using the resistor divider relation:

Vout = Vref (1+Rf2/Rf1)

Using a 1V reference voltage:
- Rf1 = 300 kΩ
- Rf2 = 600 kΩ

This produced a nominal regulated output voltage of approximately 1.5V.

pictures for dc operating point, loop gain before comp, loop gain after comp
<p align="center">
  <img src="../assets/opamp/schematic.png" width="500">
</p>
<p align="center"><em>Figure 1: Top-level schematic of the two-stage operational amplifier.</em></p>

<p align="center">
  <img src="../assets/opamp/cmfb.png" width="500">
</p>
<p align="center"><em>Figure 2: Common-mode feedback (CMFB) circuit used to regulate output common-mode level.</em></p>

---

## Key Design Parameters

| Component | Value |
|--------|--------|
| PMOS Pass Transistor | W = 7.11mm, L = 0.4 um |
| Error Amplifier Transistors |	W = 5 µm, L = 0.36 µm |
| Miller Capacitor |	300 pF |
| Miller Resistor |	50 Ω |
| Output Capacitor	| 100 pF |
| ESR Compensation Resistor	| 100 Ω |
| Bias Current Sources | 0.25 mA each |
| Supply Voltage | 2 V |

One of the major design tradeoffs encountered during the project was the relationship between stability and transient response. Improving phase margin at low load currents required aggressive compensation, which reduced oscillatory behavior but also introduced bandwidth limitations. While the compensated design achieved stable transient performance during 1mA-to-50mA load switching, the loop remained more sensitive under edge-case light-load conditions due to reduced pass transistor transconductance and shifting output pole locations.

Another important tradeoff involved quiescent power consumption versus amplifier gain and bandwidth. The error amplifier bias currents were intentionally minimized to meet the standby power requirement of less than 5mW. Final bias currents of 0.25mA per branch resulted in approximately 1mW total standby power dissipation, significantly below the design limit. However, lowering the amplifier current also reduced achievable loop gain and limited regulator bandwidth, highlighting a common tradeoff in low-power analog regulator design.

The pass transistor sizing also required balancing multiple competing objectives. Increasing device width improved current drive capability and transient response but introduced larger parasitic capacitances that complicated frequency compensation and loop stability. Shortening transistor channel length reduced output voltage peaking during transient events but increased sensitivity to stability degradation at lighter loads.

A further tradeoff explored during the project was line regulation versus low-dropout operation. Since the regulator was designed with a relatively small voltage headroom between the 2V supply and 1.5V output, maintaining accurate regulation across varying input voltages became increasingly dependent on error amplifier gain and pass transistor operation. Although line regulation was not an explicit project specification, additional DC sweep simulations were performed to evaluate regulator performance under varying supply conditions.

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

