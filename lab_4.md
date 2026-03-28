# EXPERIMENT 4:
# Analysis of MOSFET Differential Amplifier 

## Aim
To design and simulate a MOSFET differential amplifier configuration using LTspice. The project evaluates performance through DC, Transient, and AC analysis. Specificatioms:

## Introduction

A MOSFET differential amplifier is a fundamental building block in analog integrated circuits, widely used in applications such as operational amplifiers, comparators, and signal processing systems. It is designed to amplify the difference between two input signals while rejecting any signals that are common to both inputs, a property known as **common-mode rejection**.

Typically constructed using a pair of matched MOSFETs sharing a common current source, the differential amplifier operates by steering current between the two transistors based on the input voltage difference. This configuration provides high gain, good noise immunity, and improved stability compared to single-ended amplifiers.

The analysis of a MOSFET differential amplifier involves understanding its operation under both **large-signal** and **small-signal** conditions. Large-signal analysis explains how the circuit behaves for significant input differences, including current steering and saturation regions. Small-signal analysis, on the other hand, focuses on linear operation around a bias point and is used to determine parameters such as voltage gain, input resistance, and output resistance.

Because of its ability to suppress noise and amplify differential signals accurately, the MOSFET differential amplifier plays a crucial role in modern electronic circuit design.


## Theory

A differential amplifier is a circuit that amplifies the difference between two input signals while rejecting any signal that is common to both inputs. This property is known as **common-mode rejection** and is an important feature in analog circuit design.

A basic MOS differential amplifier consists of two matched MOSFETs (M1 and M2) whose sources are connected together and biased using a constant current source. The drains are connected to load elements such as resistors or active loads.

When a differential input voltage is applied:

$$
v_{id} = v_{in1} - v_{in2}
$$

the total current is steered between the two transistors depending on the input difference. If $v_{in1} > v_{in2}$, transistor M1 conducts more current, and if $v_{in2} > v_{in1}$, transistor M2 conducts more.

For small differential inputs, both transistors operate in the saturation region, and the circuit behaves linearly. The differential gain of the amplifier is given by:

$$
A_v = g_m R_{out}
$$

where $g_m$ is the transconductance of the MOSFET and $R_{out}$ is the effective output resistance.

The transconductance is defined as:

$$
g_m = \frac{2 I_D}{V_{ov}}
$$

where $I_D$ is the drain current and $V_{ov}$ is the overdrive voltage.

For larger differential inputs:

$$
v_{id} > 2 V_{ov}
$$

one transistor turns OFF while the other carries the entire current, resulting in non-linear operation.

The performance of the differential amplifier depends on the type of load used:

- **Resistive load** → moderate gain  
- **Active load** → higher output resistance and higher gain  
- **Current mirror load** → maximum gain and improved output characteristics  

Thus, by changing the circuit configuration, the gain, bandwidth, and overall performance of the differential amplifier can be significantly affected.

# Circuit 1: MOSFET Differential Amplifier (With Resistive Load)

## Working Principle of Differential Amplifier with Resistive Load

A differential amplifier with resistive load consists of two matched MOSFETs (M1 and M2) whose sources are connected together and biased by a constant current source $I_{SS}$. The drains of the transistors are connected to resistors $R_D$, which act as load elements.

### Operation

When the input voltages are equal:

$$
v_{in1} = v_{in2}
$$

the differential input voltage is zero:

$$
v_{id} = 0
$$

The tail current $I_{SS}$ is equally divided between the two transistors:

$$
I_{D1} = I_{D2} = \frac{I_{SS}}{2}
$$

As a result, the output voltages at both drains are equal, and no differential output is produced.

---

### Differential Mode Operation

When a differential input is applied:

$$
v_{id} = v_{in1} - v_{in2}
$$

- If $v_{in1} > v_{in2}$:
  - M1 conducts more current
  - M2 conducts less current
  - Voltage at drain of M1 decreases
  - Voltage at drain of M2 increases

- If $v_{in2} > v_{in1}$:
  - M2 conducts more current
  - M1 conducts less current
  - Voltage at drain of M2 decreases
  - Voltage at drain of M1 increases

Thus, the circuit converts a differential input voltage into a differential output voltage.

---

### Output Voltage

The output voltage is taken as the difference between the two drain voltages:

$$
v_{out} = v_{o1} - v_{o2}
$$

Since resistors are used as loads, the output voltage depends on the voltage drop across $R_D$:

$$
v_o = V_{DD} - I_D R_D
$$

---

### Small-Signal Operation

For small input signals, both MOSFETs operate in the saturation region. The amplifier behaves linearly, and the differential gain is given by:

$$
A_v = g_m R_D
$$

where:
- $g_m$ is the transconductance
- $R_D$ is the load resistance

---

### Key Characteristics

- Provides moderate voltage gain
- Simple circuit design
- Good linearity for small signals
- Limited gain due to finite value of $R_D$

---

Thus, a differential amplifier with resistive load works by steering current between two branches based on the input difference and converting it into output voltage variations across the load resistors.


## Circuit Diagram
<img width="1029" height="781" alt="exp4a_circuit" src="https://github.com/user-attachments/assets/352ca105-61d8-4cd8-99a8-fb8355c91f8e" />

## Design Calculations

## Given Parameters

| Parameter | Symbol | Value |
| :--- | :--- | :--- |
| **Supply Voltage (Positive)** | $V_{DD}$ | +0.9 V |
| **Supply Voltage (Negative)** | $V_{SS}$ | -0.9 V |
| **Power Constraint** | $P$ | $\le 1.8$ mW |
| **Channel Length** | $L$ | 480 nm |
| **Input CM Voltage** | $V_{ICM}$ | 0 V |
| **Output CM Voltage** | $V_{OCM}$ | 0 V |
| **Tail Node Voltage** | $V_p$ | -0.7 V |
| **Load Capacitance** | $C_L$ | 10 pF |
| **Threshold Voltage** | $V_T$ | $\approx 0.36$ V |
| **Process Parameter** | $\mu_n C_{ox}$ | 236.5 $\mu$ A/V² |


## 2. Power and Current Constraints
The total power consumption is determined by the total supply rail and the tail current ($I_{SS}$):

$$P = (V_{DD} - V_{SS}) \cdot I_{SS}$$

Given $V_{DD} - V_{SS} = 1.8$ V and $P \le 1.8$ mW:

$$1.8 \cdot I_{SS} \le 1.8 \times 10^{-3}$$

$$I_{SS} \le 1 \text{ mA}$$

To maximize performance within the budget, we select **$I_{SS} = 1$ mA**.  


## Load Resistance Calculation

Given

$$
V_{OCM} = 0 \, \text{V}
$$

So,

$$
V_{out1} = V_{out2} = 0 \, \text{V}
$$

Output Voltage Equation

The output voltage is given by:

$$
V_{out} = V_{DD} - I_D R_D
$$

Substituting Values

$$
0 = 0.9 - I_D R_D
$$

$$
I_D R_D = 0.9
$$

Solving for Load Resistance

$$
R_D = \frac{0.9}{I_D}
$$

Substituting:

$$
R_D = \frac{0.9}{0.5 \times 10^{-3}}
$$

$$
R_D = 1.8 \, \text{k}\Omega
$$

Result

$$
R_D = 1.8 \, \text{k}\Omega
$$

----
## DC Bias Point and Saturation Check

| Parameter | Calculation | Value |
| :--- | :--- | :--- |
| **Gate Voltage** | $V_G = V_{ICM}$ | 0 V |
| **Source Voltage** | $V_S = V_p$ | -0.7 V |
| **Gate-Source Voltage** | $V_{GS} = V_G - V_S$ | 0.7 V |
| **Overdrive Voltage** | $V_{OV} = V_{GS} - V_T$ | 0.34 V |
| **Drain Voltage** | $V_D = V_{OCM}$ | 0 V |
| **Drain-Source Voltage** | $V_{DS} = V_D - V_S$ | 0.7 V |

For a balanced differential pair:
$$I_{D1} = I_{D2} = \frac{I_{SS}}{2} = 0.5 \text{ mA}$$

----

## Width Calculation

The drain current in saturation is given by:

$$
I_D = \frac{1}{2} \mu_n C_{ox} \frac{W}{L} (V_{GS} - V_T)^2
$$

Rewriting:

$$
I_D = \frac{1}{2} \mu_n C_{ox} \frac{W}{L} (V_{OV})^2
$$

Rearranging to Find Width

$$
W = \frac{2 I_D L}{\mu_n C_{ox} (V_{OV})^2}
$$

Substituting Values

$$
I_D = 0.5 \, \text{mA} = 0.5 \times 10^{-3} \, \text{A}
$$

$$
L = 480 \, \text{nm} = 480 \times 10^{-9} \, \text{m}
$$

$$
\mu_n C_{ox} = 236.5 \, \mu\text{A}/\text{V}^2 = 2.365 \times 10^{-4}
$$

$$
V_{OV} = 0.34 \, \text{V}
$$

Calculation

$$
W = \frac{2 \times 0.5 \times 10^{-3} \times 480 \times 10^{-9}}{2.365 \times 10^{-4} \times (0.34)^2}
$$

$$
W = \frac{480 \times 10^{-12}}{2.365 \times 10^{-4} \times 0.1156}
$$

$$
W = \frac{480 \times 10^{-12}}{2.732 \times 10^{-5}}
$$

$$
W \approx 17.57 \, \mu\text{m}
$$


Result

$$
W \approx 17.57 \, \mu\text{m}
$$


### Simulation-Based Refinement
First-order equations do not account for channel length modulation, mobility degradation, or short-channel effects. To maintain the exact bias point of $V_p = -0.7$ V in a real TSMC 180 nm model, the width was adjusted in LTspice.

**Final Optimized Width ($W_{final}$):** $\approx 28.475\ \mu\text{m}$

------


## DC Operating Point


<img width="735" height="518" alt="image" src="https://github.com/user-attachments/assets/76e708fc-c488-4fc8-9ee3-5351f8aeea2d" />

-----


# Input and Output Common-Mode Ranges

## 1. Input Common-Mode Range (ICMR)
The ICMR is the range of input voltages for which all transistors in the differential pair remain in the saturation region and the tail current source remains active.

### Minimum Input Common-Mode Voltage ($V_{ICM,min}$)
To keep the NMOS transistors ON and the tail current source active:
$$V_{GS} \ge V_T$$
$$V_{ICM,min} = V_S + V_T$$

**Calculation:**
* $V_S = -0.7 \text{ V}$
* $V_T = 0.36 \text{ V}$
* $V_{ICM,min} = -0.7 + 0.36 = -0.34 \text{ V}$

> **Insight:** Below $-0.34 \text{ V}$, the transistors enter the cutoff region and the differential pair stops conducting.

### Maximum Input Common-Mode Voltage ($V_{ICM,max}$)
To ensure the NMOS transistors do not enter the triode region:
$$V_{DS} \ge V_{GS} - V_T \implies V_{ICM,max} = V_D + V_T$$

**Calculation:**
* $V_D = 0 \text{ V}$ (at equilibrium)
* $V_T = 0.36 \text{ V}$
* $V_{ICM,max} = 0 + 0.36 = 0.36 \text{ V}$

### Final ICMR Result
$$-0.34 \text{ V} \le V_{ICM} \le 0.36 \text{ V}$$

---

## 2. Output Common-Mode Range (OCMR)
The OCMR defines the allowable swing of the output voltage while maintaining transistor saturation.

### Maximum Output Voltage ($V_{OCM,max}$)
The maximum output is limited by the positive supply rail:
$$V_{OCM,max} \le V_{DD} = 0.9 \text{ V}$$
At this limit, the current through $R_D$ approaches zero as the output node reaches the supply rail.

### Minimum Output Voltage ($V_{OCM,min}$)
To maintain saturation at the drain ($V_{DS} \ge V_{OV}$):
$$V_D - V_S = V_{OV} \implies V_{OCM,min} = V_S + V_{OV}$$

**Calculation:**
* $V_S = -0.7 \text{ V}$
* $V_{OV} = 0.34 \text{ V}$
* $V_{OCM,min} = -0.7 + 0.34 = -0.36 \text{ V}$

### Final OCMR Result
$$-0.36 \text{ V} \le V_{OCM} \le 0.9 \text{ V}$$

---

## 3. Differential Input Range (Linear Region)
The amplifier operates linearly when current is shared between both devices and neither transistor is fully steered into cutoff.

**Condition for Linear Operation:**
$$|V_{id}| \le \sqrt{2} V_{OV}$$
Using our design value $V_{OV} = 0.34 \text{ V}$:
$$|V_{id}| \le \sqrt{2} \times 0.34 \approx 0.48 \text{ V}$$


(Note: If using the simpler approximation $|V_{id}| \le 2V_{OV}$): $|V_{id}| \le 0.68 \text{ V}$

### Final Linear Range
$$-0.48 \text{ V} \le V_{id} \le 0.48 \text{ V}$$

---

## 📝 Design Summary and Insights

| Range Type | Limitation | Importance |
| :--- | :--- | :--- |
| **ICMR** | Input bias boundaries | Defines DC biasing stability. |
| **OCMR** | Output swing boundaries | Limits the maximum undistorted output signal. |
| **Differential** | Linear gain boundaries | Determines the point where signal clipping occurs. |

-------

## Transient Analysis and Linearity Observation

The linear behavior of the differential amplifier is verified using transient analysis.

---

### Condition for Linearity

$$
|V_{id}| < 2 V_{OV}
$$

$$
2 V_{OV} = 1.414 \times 0.34 = 0.48 \, \text{V}
$$

---

### Case 1: Linear Region

Input applied:

$$
V_{id} = 100 \, \text{mV} < 0.48 \, \text{V}
$$


<img width="1540" height="645" alt="image" src="https://github.com/user-attachments/assets/c8653f20-fb4e-4c91-931c-29add1e864d6" />

### Case 2: Non-Linear Region

Input applied:

$$
V_{id} = 600 \, \text{mV} > 0.48 \, \text{V}
$$


<img width="1537" height="646" alt="image" src="https://github.com/user-attachments/assets/df14fd88-c936-4ca2-8cb3-d8f4d71fc584" />

### Linearity Verification
Checking the boundary condition:
$$|V_{id}| > 2V_{OV}$$
$$800\text{ mV} > 680\text{ mV} \implies \text{Non-Linear Region}$$

### Expected Observations & Interpretation
* **Distortion:** The output waveform exhibits heavy clipping at the peaks.
* **Current Steering:** Large input forces nearly all current ($I_D \approx I_{SS}$) into one transistor, pushing the other into **cutoff**.
* **Symmetry:** The outputs lose sinusoidal symmetry as the circuit reaches its physical current limits.
* **Result:** The circuit behaves more like a **switch** than an amplifier; gain becomes non-linear and input-dependent.

---

## Comparison Summary

| Parameter | Linear Operation | Non-Linear Operation |
| :--- | :--- | :--- |
| **Condition** | $|V_{id}| < 2V_{OV}$ | $|V_{id}| > 2V_{OV}$ |
| **Input Magnitude** | 100 mV | 800 mV |
| **Output Shape** | Sinusoidal | Distorted / Clipped |
| **Gain** | Constant | Non-linear |
| **Transistor State** | Both in Saturation | One in Cutoff |
| **Current Distribution** | Shared | Fully Steered |

---

## Key Design Insight
The linear range of a differential amplifier is finite and strictly defined by the overdrive voltage:
$$|V_{id}|_{max} = 2V_{OV}$$
Beyond this limit, the amplifier loses its proportional relationship between input and output, transitioning into switching behavior. Proper design requires selecting a $V_{OV}$ that accommodates the expected peak signal swing.

## Conclusion
The transient analysis confirms that for $V_{id} = 100\text{ mV}$, the amplifier operates as intended. Increasing the input to $800\text{ mV}$ successfully demonstrates the non-linear boundaries of the TSMC 180nm NMOS pair.

# Theoretical and Simulated Gain Analysis

The performance of the differential amplifier is evaluated by comparing analytical calculations with time-domain simulation results.

---

## 1. Simulated Gain Calculation

### Input Signal Configuration
* **Waveform Type:** Sine Wave
* **Frequency:** 1 kHz
* **Amplitude:** 50 mV (per branch)
* **DC Offset:** 0.1 V
* **Peak Differential Input ($V_{id}$):** 100 mV

  <img width="1894" height="403" alt="image" src="https://github.com/user-attachments/assets/98836b51-84d4-4cb8-be88-5a0ee7ba2fab" />


### Measured Values from Simulation
The peak-to-peak voltages were extracted from the LTspice transient analysis:

* **Input Peak-to-Peak ($V_{in,pp}$):** $$V_{in,pp} = 50\text{ mV} - (-50\text{ mV}) = 100\text{ mV}$$
* **Output Peak-to-Peak ($V_{out,pp}$):** $$V_{out,pp} = 287.165\text{ mV} - (-287.165\text{ mV}) = 574.33\text{ mV}$$

### Calculated Voltage Gain ($A_v$)
The voltage gain in linear and decibel scales is:
$$A_v = \frac{V_{out,pp}}{V_{in,pp}} = \frac{574.33 \times 10^{-3}}{100 \times 10^{-3}} = 5.74$$

**Gain in dB:**
$$A_v(dB) = 20 \log_{10}(5.74) \approx 15.18\text{ dB}$$

---

## 2. Theoretical Gain Comparison

Based on the small-signal model ($A_d \approx g_m R_D$), the theoretical gain was calculated in the previous design section.

### Updated Performance Summary

| Parameter | Theoretical Value | Simulated Value |
| :--- | :--- | :--- |
| **Voltage Gain (V/V)** | 4.5 | 5.74 |
| **Voltage Gain (dB)** | 13.06 dB | 15.18 dB |

---


# AC Analysis: Frequency Response and Bandwidth

AC analysis is performed to evaluate the frequency response, midband gain, and bandwidth of the MOSFET differential amplifier. This determines the high-frequency limitations of the design.

---

## 1. Simulation Setup
To extract the differential frequency response, the following parameters were used in LTspice:

* **Command:** `.ac dec 100 1 10G`
* **Differential Excitation:** * `Vin1`: AC 1
  * `Vin2`: AC -1
* **Output Measurement:** `V(out1) - V(out2)`

  <img width="1919" height="978" alt="image" src="https://github.com/user-attachments/assets/92b2e4c6-caa1-4567-913b-ee74f36af1a9" />


---

## 2. Simulation Results

### Midband Gain ($A_v$)
Extracted from the flat region of the Bode plot:
* **Decibel Scale:** $A_v = 15.6\text{ dB}$
* **Linear Scale:** $A_v \approx 6.02\text{ V/V}$

> **Note:** This result closely aligns with the transient analysis gain ($\approx 5.74\text{ V/V}$), confirming consistency across simulation modes.

### Bandwidth (BW)
The bandwidth is determined by identifying the -3dB cutoff frequency ($f_H$):
* **-3dB Gain Point:** $15.6\text{ dB} - 3\text{ dB} = 12.6\text{ dB}$
* **Upper Cutoff Frequency ($f_H$):** $5.128\text{ GHz}$
* **Lower Cutoff Frequency ($f_L$):** $\approx 0\text{ Hz}$ (DC coupled)
* **Total Bandwidth:** $BW = f_H - f_L = 5.128\text{ GHz}$

### Unity Gain Bandwidth (UGB)
The Unity Gain Bandwidth is the frequency where the gain drops to $0\text{ dB}$ ($1\text{ V/V}$):
$$UGB \approx A_{v,linear} \times BW$$
$$UGB = 6.02 \times 5.128\text{ GHz} \approx 30.9\text{ GHz}$$

---

## 3. Interpretation and Insights

* **Flat Midband Region:** The stable gain across lower frequencies indicates proper DC biasing and a lack of significant coupling capacitor effects.
* **High-Frequency Roll-off:** The gain begins to decrease at extremely high frequencies due to internal MOSFET parasitic capacitances ($C_{gs}$, $C_{gd}$) and the 10 pF load capacitance ($C_L$).
* **Speed Performance:** A bandwidth in the GHz range confirms that this TSMC 180nm differential pair is suitable for high-speed analog signal processing.
* **Gain-Bandwidth Trade-off:** The high UGB of $30.9\text{ GHz}$ highlights the capability of the technology node when biased at the power limit of $1.8\text{ mW}$.

---

## 🚀 Summary of AC Performance

| Metric | Value |
| :--- | :--- |
| **Midband Gain ($A_v$)** | $15.6\text{ dB}$ |
| **-3dB Bandwidth ($f_H$)** | $5.128\text{ GHz}$ |
| **Unity Gain Bandwidth** | $\approx 30.9\text{ GHz}$ |

**Conclusion:** The AC analysis validates that the amplifier provides moderate gain and exceptionally wide bandwidth, confirming the stability and high-speed efficiency of the design.




