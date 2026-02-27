<h1 style="font-size:30px;">Experiment-1</h1>


<h1 style="font-size:25px;">Common Source amplifier analysis-1</h1>


This experiment shows the ac,dc and transient analysis of cs amplifier



<h1 style="font-size:25px;">Theory</h1>
# Common Source (CS) Amplifier – Theory

## Introduction

A **Common-Source (CS) amplifier** is a widely used MOSFET amplifier configuration in which:

- The input is applied to the **gate**
- The output is taken from the **drain**
- The **source** acts as the common terminal

It provides voltage amplification by varying the drain current ($I_D$) in response to changes in the gate-to-source voltage ($V_{GS}$).

The output signal is **180° out of phase** with the input signal, meaning the amplifier produces an inverted output.

The CS amplifier has:

- High input impedance (because gate current is nearly zero)
- Moderate to high output impedance

---

## Conditions for Proper Operation

For correct amplification, the MOSFET must operate in the **saturation region**.

The required conditions are:

1. $V_{GS} \geq V_{th}$  
   → To turn the transistor ON  

2. $V_{DS} > V_{GS} - V_{th}$  
   → To keep the transistor in saturation  

3. The input signal $v_{in}$ must be small  
   → To ensure small-signal operation  

4. Proper biasing and correct selection of $R_D$  
   → To obtain stable operation and sufficient voltage gain  

---

## Drain Current in Saturation Region

In the saturation region, the drain current is given by:

$$
I_D = \frac{1}{2} k_n (V_{ov})^2
$$

where,

$$
V_{ov} = V_{GS} - V_{th}
$$

$k_n$ = Process transconductance parameter  

---

## Small-Signal Voltage Gain

The voltage gain of a CS amplifier is:

$$
A_v = -g_m R_D
$$

where,

$$
g_m = \frac{2 I_D}{V_{ov}}
$$

The negative sign indicates **phase inversion**.

<h1 style="font-size:25px;">Circuit</h1>
<img width="575" height="470" alt="Screenshot 2026-02-27 124937" src="https://github.com/user-attachments/assets/3d85013e-d2b7-4d66-935c-c0455088431e" />

## Given Design Requirements

| Parameter | Symbol | Value | Unit | Description |
|------------|---------|--------|------|-------------|
| Supply Voltage | VDD | 1.8 | V | DC power supply |
| Maximum Power | Pmax | ≤ 1 | mW | Power constraint |
| Load Capacitance | CL | 10 | pF | Output load |
| NMOS Channel Length | Ln | 560 | nm | Technology parameter |
| Technology Node | — | 180 | nm | CMOS process |
| Simulation Tool | — | LTspice | — | Design environment |

---

## Derived Parameter (From Power Constraint)

| Parameter | Formula | Calculated Value | Unit |
|------------|----------|------------------|------|
| Maximum Drain Current | ID ≤ Pmax / VDD | ≤ 0.5555 | mA |

<h1 style="font-size:25px;">Dc Analysis</h1>
## DC Analysis in Common Source (CS) Amplifier

### DC Analysis of a Common Source (CS) Amplifier

**DC analysis of a Common Source (CS) amplifier** is performed to determine the operating point (Q-point) of the MOSFET when no AC signal is applied. In this analysis, coupling and bypass capacitors are treated as open circuits, and only the biasing network is considered. The gate voltage is set by the bias resistors, which establishes the gate-to-source voltage $(V_{GS})$. This controls the drain current $(I_D)$, provided the MOSFET operates in the saturation region. The drain voltage $(V_D)$ is then found using $(V_D = V_{DD} - I_D R_D)$. Proper DC biasing ensures the transistor remains in saturation and allows the amplifier to provide undistorted amplification of the input signal.
<img width="575" height="470" alt="Screenshot 2026-02-27 124937" src="https://github.com/user-attachments/assets/e8983955-fb66-4754-848b-c0183d2a9409" />


# Simulated DC Operating Point Results

| Parameter | Symbol | Simulated Value | Unit |
|------------|---------|----------------|------|
| Supply Voltage | VDD | 1.8 | V |
| Input Voltage | Vin | 0.9 | V |
| Output Voltage | Vout | 0.901 | V |
| Drain Current | ID | 0.199 | mA |
| Current through RD | I(RD) | 0.199 | mA |
| Supply Current | I(VDD) | 0.199 | mA |

---

## Power Calculation

P = VDD × ID  

P = 1.8 × 0.199 mA  

P = 0.3582 mW

# Transient Analysis of Common Source (CS) Amplifier

## Introduction
### Transient Analysis of a Common Source (CS) Amplifier

Transient analysis of a Common Source (CS) amplifier examines the time-domain response of the circuit when an input signal is applied. It shows how the output voltage changes with respect to time for varying input signals such as step, pulse, or sinusoidal waveforms. During transient analysis, capacitors (coupling and bypass capacitors) are considered in their charging and discharging states, affecting the rise time, fall time, and overall signal shape. The MOSFET responds to changes in gate-to-source voltage $(V_{GS})$ , causing corresponding variations in drain current $(I_D)$ and output voltage. This analysis helps evaluate signal amplification, phase inversion, delay, and distortion under dynamic conditions.
## Voltage Gain Measurement

Voltage gain is calculated using peak values:

$$
A_v = \frac{V_{out}}{V_{in}}
$$

Since the CS amplifier inverts the signal:

$$
A_v = - \frac{V_{out}}{V_{in}}
$$

## 1. Input Waveform (V_in)

<img width="1365" height="603" alt="Screenshot 2026-02-27 125725" src="https://github.com/user-attachments/assets/0217ebb3-1d3f-4625-8e86-ec6a44003168" />

## 2. Output Waveform (V_out)
<img width="1364" height="720" alt="Screenshot 2026-02-27 125117" src="https://github.com/user-attachments/assets/d2f9dcb0-2a41-42ff-b0af-6733edfcd45f" />

Voltage gain:

$$
A_v = \frac{V_{out(pp)}}{V_{in(pp)}}
$$

$$
A_v = \frac{63.909}{19.237}
$$

$$
A_v \approx 3.333
$$

Since the Common Source amplifier produces phase inversion:

$$
A_v \approx -3.33
$$

### Reason for Negative Gain

The gain is negative because the Common Source amplifier inverts the signal.  
When the input voltage increases, the drain current increases, causing a larger voltage drop across $R_D$, which reduces the output voltage.  
Thus, the output is 180° out of phase with the input.

# DC Sweep Analysis – Common Source Amplifier

## Objective
### Objective of DC Sweep

The objective of DC sweep analysis is to examine how the output characteristics of a circuit change as a DC source (such as voltage or current) is varied over a specified range. In a Common Source (CS) amplifier, DC sweep is used to study the relationship between parameters like drain current $(I_D)$ and drain-to-source voltage $(V_{DS})$, or between $(I_D)$ and gate-to-source voltage $(V_{GS})$. This analysis helps in determining the operating region of the MOSFET, plotting characteristic curves, and selecting a proper Q-point for stable and efficient amplifier operation.

<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/37d21871-b1a1-4c50-ba1d-c4a52da93c5b" />

## AC Analysis

### AC Analysis of a Common Source (CS) Amplifier

AC analysis of a Common Source (CS) amplifier is performed to determine its frequency response and voltage gain under small-signal conditions. In this analysis, DC sources are set to zero (AC ground), and coupling and bypass capacitors are treated as short circuits at mid frequencies. The MOSFET is replaced with its small-signal model to calculate parameters such as voltage gain $(A_v)$, input impedance, and output impedance. AC analysis helps evaluate how the amplifier responds to different signal frequencies, identify the bandwidth, and determine the lower and upper cutoff frequencies for proper signal amplification.


<img width="1919" height="1079" alt="image" src="https://github.com/user-attachments/assets/6115460c-28df-430c-b695-957109ce5950" />


   Theoretical Gain:

   Gain $(A_v)$ = $g_m)$ x $(R_d)$ = (2 x $(I_d)$ x $(R_d)$/ $(V_ov)$
                  = (2 x 200E-6 x 4.5E3)/(0.9-0.36)
                  = 3.33

   $(A_v)$ dB = 20log $(A_v)$
              = 20log(3.33) = 10.45 dB

   Practical Gain is observed to be 10.4 dB.

   The theoretical and practical values of gain are observed to be nearly matching, which indicates proper design and accurate biasing of the MOSFET amplifier. The theoretical gain is calculated using ideal device equations by neglecting parasitic effects, whereas the practical or simulated gain includes second-order effects such as channel length modulation, parasitic capacitances, and device model parameters. The close agreement between both values confirms that the amplifier operates correctly in the saturation region and validates the design assumptions and calculations.



### Result

The Common Source (CS) amplifier was successfully analyzed using DC, AC, transient, and DC sweep analyses. The DC analysis established a proper Q-point in the saturation region for stable operation. The AC analysis confirmed that the amplifier provides high voltage gain with a 180° phase shift between input and output. Transient analysis verified correct time-domain response and signal amplification without significant distortion. The DC sweep analysis illustrated the characteristic curves and operating region of the MOSFET. Overall, the CS amplifier demonstrated effective voltage amplification as expected.









