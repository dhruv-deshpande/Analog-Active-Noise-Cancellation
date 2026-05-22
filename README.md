# Analog Active Noise Cancellation (ANC) System

A hardware-based analog Active Noise Cancellation (ANC) system designed to attenuate predictable low-frequency ambient noise (such as fan hum or motor noise) using real-time analog signal processing. The circuit conditions a reference noise input, applies a calculated phase delay, and generates an inverted "anti-noise" signal to achieve destructive interference.

> **Project Context:** Developed as an Electronic System Design Project (ESDP) for the 4th-semester ECE curriculum at MIT, Manipal. 

---

## My Core Technical Contributions & Ownership
While the attached engineering report represents the final collaborative team submission, I personally owned and executed the core technical phases of this project:

* **Circuit Simulation & Optimization (LTspice):** Designed, modeled, and verified the complete multi-stage schematic. Performed transient analysis (`.tran 0 10m 0 1u`) to validate exact signal inversion and accurate signal blending.
* **Hardware Prototyping & Debugging:** Independently constructed the active op-amp networks on the breadboard. Successfully debugged power supply noise issues by implementing RC decoupling networks on the $V_{DD}$ rails.
* **Mathematical Modeling:** Calculated and tuned the passive component networks ($R$ and $C$ values) to match the required acoustic delay line.

---

## Circuit Architecture & Engineering Specs

The entire system is implemented using **LT741 operational amplifiers** ($\times 4$) distributed across three primary functional blocks:

### 1. Microphone Pre-Amplifier
Boosts the low-voltage AC signal from the input electret microphone to a usable processing level. 
* **Configuration:** Inverting Amplifier
* **AC Gain:** 22 ($\frac{R_3}{R_2} = \frac{22\text{ k}\Omega}{1\text{ k}\Omega}$)
* **Signal Conditioning:** Includes a coupling capacitor to block DC offsets and an RC filter network ($2.2\ \Omega$ and $10\ \mu\text{F}$) on the supply lines to suppress high-frequency ripple.

### 2. All-Pass Filter (Phase Delay Stage)
Introduces a precise time delay to align the phase of the processed electrical anti-noise signal with the acoustic noise wave traveling through the air at the speed of sound ($V_s = 340\text{ m/s}$).
* **Formula:** $t \approx \frac{L}{V_s}$ and $\Delta\phi = 2\pi ft$
* **Hardware Implementation:** Tuned using a precise RC network ($1\text{ nF}$ capacitors and $13\text{ k}\Omega$ / $10\text{ k}\Omega$ resistors) to achieve target phase shift without affecting signal magnitude.

### 3. Summing Amplifier & Output Stage
Combines the desired audio/music input with the conditioned anti-noise signal.
* **Music Path Gain:** 1 ($\frac{R_8}{R_{10}} = \frac{10\text{ k}\Omega}{10\text{ k}\Omega}$)
* **Noise Path Gain:** 0.0425 ($\frac{R_8}{R_7} = \frac{10\text{ k}\Omega}{235\text{ k}\Omega}$)
* **Operation:** Utilizes an inverting configuration to create the exact negative "anti-noise" wave needed for destructive superposition, leaving the music intact while attenuating the ambient profile.

---

## System Components Used
* **Active Devices:** LT741 Operational Amplifiers
* **Passives:** $1\text{ nF}$ and $10\ \mu\text{F}$ Capacitors; $100\ \Omega$, $1\text{ k}\Omega$, $10\text{ k}\Omega$, $13\text{ k}\Omega$, $22\text{ k}\Omega$, $235\text{ k}\Omega$, and $1\text{ M}\Omega$ Resistors
* **Instrumentation:** Dual $\pm12\text{V}$ Power Supply, Function Generator, Oscilloscope

---

## Future Improvements
* **Adaptive Filtering:** Transition from a fixed analog RC delay line to a digital adaptive filtering algorithm (such as the LMS algorithm) to handle dynamic, multi-frequency ambient environments.
* **Multi-Frequency Arrays:** Expand the single-stage all-pass network into a multi-stage active filter network to handle higher-frequency noise spectrums.
