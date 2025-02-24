# Power (Static & Dynamic) Interview Questions and Answers

## 1. What are the different types of power dissipation in a digital circuit?

Power dissipation in a digital circuit is categorized into:

- **Static Power**: Power consumed when the circuit is idle (leakage power).
- **Dynamic Power**: Power consumed due to switching activity.

---

## 2. What are the major sources of static power consumption?

Static power consumption occurs due to:

- Leakage current in transistors.
- Subthreshold leakage (when transistors are partially ON).
- Gate-oxide leakage due to tunneling effects.
- Junction leakage in reverse-biased PN junctions.

---

## 3. What are the major sources of dynamic power consumption?

Dynamic power consumption occurs due to:

- Charging and discharging of capacitive loads.
- Short-circuit current flowing between VDD and GND during switching.
- Glitches and unnecessary switching activity in combinational circuits.

---

## 4. What is the formula for dynamic power consumption?

The dynamic power consumption is given by:

\[
P_{dynamic} = \alpha C V^2 f
\]

where:
- \( \alpha \) = Activity factor (probability of switching)
- \( C \) = Load capacitance
- \( V \) = Supply voltage
- \( f \) = Clock frequency

---

## 5. How does reducing the supply voltage affect power consumption?

- Dynamic power is proportional to \( V^2 \), so reducing voltage significantly decreases power consumption.
- Lowering voltage also reduces leakage power but may impact circuit performance.

---

## 6. What is clock gating, and how does it help in reducing power?

Clock gating reduces dynamic power by:

- Disabling the clock signal for inactive logic blocks.
- Preventing unnecessary switching activity.
- Implementing enable-controlled clock buffers.

---

## 7. What are the challenges in implementing clock gating?

- Improper clock gating may cause glitches.
- Additional logic delay due to enable signal propagation.
- Need for timing verification in gated clock paths.

---

## 8. How does multi-voltage design help in power reduction?

Multi-voltage design uses different supply voltages for different blocks:

- High-performance blocks operate at higher voltage.
- Low-power blocks operate at reduced voltage.
- Level shifters are used to interface between different voltage domains.

---

## 9. What is dynamic voltage and frequency scaling (DVFS)?

DVFS adjusts voltage and frequency based on workload:

- Reduces power during low activity.
- Increases performance when required.
- Used in modern processors and mobile SoCs for power efficiency.

---

## 10. What is the impact of reducing clock frequency on power consumption?

- Dynamic power is directly proportional to frequency.
- Reducing frequency lowers switching activity and power consumption.
- Performance may degrade if frequency is reduced too much.

---

## 11. What are retention cells, and how do they help in low-power design?

- Retention cells hold state information when power is turned off.
- Used in power gating to retain essential data.
- Avoids the need for full re-initialization after wake-up.

---

## 12. What is power gating, and how does it reduce leakage power?

Power gating reduces leakage power by:

- Turning off unused circuit blocks.
- Using high-Vt transistors as power switches.
- Implementing power switches at domain boundaries.

---

## 13. What are the challenges in power gating?

- Increased wake-up latency due to power domain reactivation.
- Inrush current issues when power is restored.
- Complexity in state retention mechanisms.

---

## 14. What are the differences between power gating and clock gating?

- **Power gating** completely turns off power, reducing leakage power.
- **Clock gating** only disables the clock signal, reducing dynamic power.
- Power gating requires additional circuitry for wake-up, whereas clock gating has minimal impact on wake-up time.

---

## 15. How does increasing threshold voltage (Vt) affect power consumption?

- Higher \( V_t \) reduces subthreshold leakage, lowering static power.
- Higher \( V_t \) increases delay, reducing circuit performance.
- Low-power designs use high-\( V_t \) cells for non-critical paths.

---

## 16. What are the techniques used to reduce glitch power?

Glitches cause unnecessary power consumption. Techniques to reduce glitch power include:

- Using balanced path delays to avoid unnecessary transitions.
- Retiming logic to align critical paths.
- Minimizing redundant logic transitions using gated clock designs.

---

## 17. What is the role of decoupling capacitors in power management?

- Decoupling capacitors reduce voltage fluctuations (IR drop).
- They provide transient current to avoid power noise issues.
- Used in power-sensitive designs like CPUs and RF circuits.

---

## 18. What is the significance of power-aware synthesis?

Power-aware synthesis optimizes design to reduce power by:

- Choosing low-power cells and gates.
- Optimizing logic for minimal switching activity.
- Using power-reduction constraints in synthesis tools.

---

## 19. How do you perform power estimation in an ASIC design?

Power estimation is done using:

- **Pre-layout estimation** using RTL power analysis.
- **Post-layout estimation** using extracted parasitics.
- Dynamic power analysis using switching activity from simulations.

---

## 20. How does IR drop impact power integrity, and how is it minimized?

IR drop occurs due to resistive voltage drops in the power grid, causing:

- Reduced performance due to lower voltage at transistors.
- Increased risk of timing failures.

Ways to minimize IR drop:

- Optimizing power grid design with sufficient metal layers.
- Placing decoupling capacitors near high-switching logic.
- Reducing peak current demand using power-aware design strategies.

---