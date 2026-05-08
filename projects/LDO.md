# Design and Compensation of a 1.5V CMOS Low Dropout (LDO) Voltage Regulator

## Problem Statement
Designed a transistor-level 1.5V Low Dropout (LDO) voltage regulator in LTspice for a power management course final project. The objective was to maintain a regulated 1.5V output across varying load conditions while satisfying multiple analog performance constraints, including a maximum load current of 100mA, output voltage peaking below 100mV during 1mA-to-50mA load transients, load regulation better than 1%, standby error amplifier power consumption below 5mW, and operation with a fixed 100pF output capacitor. The project required complete small-signal and transient simulation verification, including pulsed load current testing with 1µs rise and fall times. The primary design challenge involved balancing transient response, loop stability, and low standby power while maintaining regulation across a wide load current range.

---

## Semester 1: Memristor Device Characterization

### Objective
To experimentally characterize memristor devices fabricated by the research
team, focusing on electroforming, resistive switching behavior, and control of
switching dynamics.

### Experimental Setup
- Optical inspection using Sanjscope microscope
- Electrical probing via probe station
- Measurements performed using Keysight B1500A Semiconductor Device Analyzer
- Direct probing of on-chip pads on memristor test structures

<p align="center">
  <img src="../assets/samsung/memristor/device.png" width="600">
</p>
<p align="center"><em>Figure 1: Optical image of the memristor device under test.</em></p>

<p align="center">
  <img src="../assets/samsung/memristor/probing.png" width="600">
</p>
<p align="center"><em>Figure 2: Probe station setup used for electrical characterization.</em></p>

---

### Measurements & Results

<p align="center">
  <img src="../assets/samsung/memristor/electroforming.png" width="600">
</p>
<p align="center"><em>Figure 3: Electroforming behavior observed during initial device activation.</em></p>

<p align="center">
  <img src="../assets/samsung/memristor/switching.png" width="600">
</p>
<p align="center"><em>Figure 4: Bipolar resistive switching behavior after successful electroforming.</em></p>

<p align="center">
  <img src="../assets/samsung/memristor/compliance.png" width="600">
</p>
<p align="center"><em>Figure 5: Controlled modulation of switching behavior using different compliance currents.</em></p>

---

### Key Outcomes
- Successfully electroformed memristor devices
- Demonstrated repeatable resistive switching behavior
- Established control over switching magnitude via compliance current tuning
- Gained hands-on experience with semiconductor device characterization tools

---

## Semester 2: 3D NAND Flash Parameter Extraction PCB

### Objective
To design and implement a custom testbench PCB capable of interfacing with and
extracting electrical parameters from a Micron 3D NAND Flash device.

### Testbench Architecture
- NAND Flash housed in a BGA-132 socket
- FTDI FT2232 board used for USB-to-serial communication with host computer
- Two TXB0108 level shifters for 3.3V to 1.2V signal translation
- On-board DC-DC regulator converting 5V to 1.2V for NAND core supply
- Pull-up and pull-down resistors for signal conditioning

---

### PCB Design & Iteration
The PCB design underwent two iterations to address signal integrity and
interface reliability challenges identified during bring-up.

<p align="center">
  <img src="../assets/samsung/nand/schematic.png" width="600">
</p>
<p align="center"><em>Figure 1: Final schematic of the NAND Flash testbench PCB.</em></p>

<p align="center">
  <img src="../assets/samsung/nand/layout.png" width="600">
</p>
<p align="center"><em>Figure 2: Final PCB layout implementing the NAND Flash test interface.</em></p>

---

### Final Implementation
The final board successfully interfaced with the NAND Flash device and enabled
parameter extraction through the custom test setup.

<p align="center">
  <img src="../assets/samsung/nand/assembled.png" width="600">
</p>
<p align="center"><em>Figure 3: Assembled NAND Flash testbench PCB.</em></p>

---

### Key Outcomes
- Designed a functional testbench PCB for advanced memory devices
- Gained experience interfacing with high-density NAND Flash packages
- Learned practical challenges of voltage level translation and PCB iteration
- Developed hardware to support silicon-level characterization


