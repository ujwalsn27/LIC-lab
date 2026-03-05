# Experiment 2: CS Amplifier
---

## Aim

Implementation of a Common Source (CS) amplifier with NMOS source degeneration and PMOS active load using LTSpice.

### Design Specifications

- **Supply Voltage:** $V_{DD} = 1.8\text{ V}$
- **Power Constraint:** $P \le 1\text{ mW}$

The design achieves proper biasing and amplification performance. The following analyses are performed:

- DC Operating Point Analysis  
- Transient Response Analysis  
- Voltage Gain Extraction  
- Bandwidth Evaluation  

---

# Theory

The Common Source (CS) amplifier is a fundamental MOSFET-based voltage amplifier configuration widely used in analog circuit design due to its ability to provide significant voltage gain. In this topology, the input signal is applied at the gate terminal of the NMOS transistor, the output is obtained from the drain terminal, and the source terminal acts as the common reference node.

In this implementation, the conventional drain resistor is replaced by a PMOS transistor functioning as an active load. Additionally, a resistor is connected at the source terminal of the NMOS device to introduce source degeneration, which enhances bias stability and linearity.

---

## PMOS as Active Load

The source of the PMOS is connected to $V_{DD}$ and its gate is biased with a fixed DC voltage to ensure saturation operation.

### Advantages

- High small-signal output resistance  
- Improved voltage gain  
- Reduced silicon area in IC implementation  

---

## Effect of Source Degeneration ($R_S$)

When drain current increases, the voltage across $R_S$ increases. This raises the source potential and reduces $V_{GS}$, stabilizing the operating point.

### Benefits

- Improved DC bias stability  
- Reduced distortion  
- Enhanced linearity  
- Reduced process sensitivity  

---

## Biasing and Saturation Conditions

### NMOS Condition

$$
V_{DS} \ge V_{OV}
$$

$$
V_{OV} = V_{GS} - V_{TH}
$$

### PMOS Condition

$$
V_{SD} \ge V_{OV}
$$

The output is biased near mid-supply for maximum symmetrical swing.

---

## Small-Signal Voltage Gain

$$
A_v \approx \frac{-g_m r_o}{1 + g_m R_S}
$$

Where:

- $g_m$ = Transconductance  
- $r_o$ = Output resistance  
- $R_S$ = Source degeneration resistor  

The negative sign indicates 180° phase inversion.

---

# Working Principle

When a small AC signal is applied at the gate:

$$
i_d = g_m v_{gs}
$$

The output voltage becomes:

$$
v_{out} = - i_d R_{out}
$$

With source degeneration:

$$
A_v \approx \frac{-g_m r_o}{1 + g_m R_S}
$$

---
## Circuit Diagram
<img width="1272" height="564" alt="image" src="https://github.com/user-attachments/assets/21ffbe12-631c-4d47-9d60-d02b2eaed032" />


# Design

## Given Parameters

- $t_{ox} = 4.1 \times 10^{-9}\text{ m}$  
- $\mu_n = 273.809 \times 10^{-4}\text{ m}^2/\text{Vs}$  
- $\varepsilon_{ox} = 3.5416 \times 10^{-11}\text{ F/m}$  
- $V_{TH} = 0.36\text{ V}$  

---

## Power Constraint

$$
P = V_{DD} \cdot I_D \le 1\text{ mW}
$$

$$
1.8 \cdot I_D \le 10^{-3}
$$

$$
I_D \le 555.5\mu A
$$

Chosen:

$$
I_D = 200\mu A
$$

$$
P = 1.8 \times 200\mu A = 0.36\text{ mW}
$$

---

## Overdrive Voltage

$$
V_{OV} = 0.25\text{ V}
$$

$$
V_{GS} = V_{OV} + V_{TH}
$$

$$
V_{GS} = 0.25 + 0.36 = 0.61\text{ V}
$$

---

## Biasing for Maximum Swing

$$
V_{DS} = \frac{V_{DD}}{2} = 0.9\text{ V}
$$

Since $0.9 \ge 0.25$, NMOS operates in saturation.

---

## Gate Voltage

$$
V_G = V_{GS} + V_{RS}
$$

$$
V_G = 0.61 + 0.2 = 0.81\text{ V}
$$

---

## Source Degeneration Resistor

$$
V_{RS} = I_D R_S
$$

$$
0.2 = 200 \times 10^{-6} \times R_S
$$

$$
R_S = 1k\Omega
$$

---

## PMOS Gate Bias

$$
V_{SG} = V_{OVp} + |V_{TP}|
$$

$$
V_{SG} = 0.25 + 0.39 = 0.64\text{ V}
$$

$$
V_G = 1.8 - 0.64 = 1.16\text{ V}
$$

$$
V_{OUT} \approx 1.1\text{ V}
$$

---

# Transistor Width Calculation

$$
I_D = \frac{1}{2} \mu_n C_{ox} \frac{W}{L} (V_{OV})^2
$$

$$
W = \frac{2 I_D L}{\mu_n C_{ox} (V_{OV})^2}
$$

Target:

$$
I_D = 200\mu A
$$

### NMOS

Initial:

$$
W_n \approx 15.15\mu m
$$

Adjusted:

$$
W_n = 56.159\mu m
$$

### PMOS

Initial:

$$
W_p \approx 35.91\mu m
$$

Adjusted:

$$
W_p = 82.1\mu m
$$

---

# DC Analysis
<img width="1339" height="516" alt="image" src="https://github.com/user-attachments/assets/bf9cbd57-528e-45fc-bf33-baece861c836" />


- $V_G \approx 0.81\text{ V}$  
- $V_S \approx 0.199\text{ V}$  
- $V_{GS} \approx 0.611\text{ V}$  
- $I_D \approx 199\mu A$  
- $V_{OUT} \approx 1.108\text{ V}$  

---

# Transient Analysis
<img width="1363" height="542" alt="image" src="https://github.com/user-attachments/assets/3da8a619-f211-4a60-bcb1-50060108389d" />

Input:

- 1 kHz sine wave  
- 10 mV amplitude  
- 0.81 V DC offset  

$$
V_{in(pp)} = 19.99\text{ mV}
$$

$$
V_{out(pp)} = 0.51523\text{ V}
$$

$$
A_v = \frac{0.51523}{19.99 \times 10^{-3}} = 25.77
$$

$$
A_v(dB) = 20 \log_{10}(25.77) = 28.22\text{ dB}
$$

---

# Theoretical Gain

$$
g_m = \frac{2I_D}{V_{OV}} = 1.6\text{ mS}
$$

$$
r_o = \frac{1}{\lambda I_D} = 50k\Omega
$$

$$
r_{out} = 25k\Omega
$$

$$
A_v = 15.38
$$

$$
A_v(dB) = 23.739\text{ dB}
$$

---

# AC Analysis
<img width="1349" height="545" alt="image" src="https://github.com/user-attachments/assets/f73b4af7-6918-4a48-b1a9-b11a49446504" />


- Midband Gain ≈ 28 dB  
- −3 dB Gain ≈ 25.4 dB  
- $f_H \approx 37.66\text{ MHz}$  

Bandwidth:

$$
BW \approx 37\text{–}40\text{ MHz}
$$

## -3 dB Cutoff Frequency (Bandwidth)
<img width="1347" height="581" alt="image" src="https://github.com/user-attachments/assets/44edda13-16dd-4c38-9f1c-a39fc2de254c" />


From the AC analysis, the midband gain of the amplifier is approximately 28 dB.  
The −3 dB point occurs when the gain drops by 3 dB from its midband value.

Midband Gain ≈ 28.4 dB  
−3 dB Gain Level ≈ 25.4 dB  

From the Bode plot, this occurs at:

$(f_H)$ ≈ 37.15 MHz

This frequency represents the **upper cutoff frequency** of the amplifier.

Beyond this point, the gain starts decreasing rapidly due to internal MOSFET parasitic capacitances (Cgs, Cgd) which introduce dominant poles in the circuit.

Hence, the bandwidth of the amplifier is approximately:

Bandwidth ≈ 37.15 MHz



---

# Inference

- $V_{DD} = 1.8\text{ V}$  
- $I_D \approx 200\mu A$  
- $P \approx 0.36\text{ mW}$  
- Theoretical Gain ≈ 15.38 V/V  
- Simulated Gain ≈ 25–28 V/V  
- Bandwidth ≈ 37–40 MHz  

The CS amplifier successfully meets the power constraint, maintains saturation operation, achieves high gain using an active load, and demonstrates improved linearity due to source degeneration.

---
