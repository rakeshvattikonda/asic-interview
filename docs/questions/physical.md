# Physical Design (PD) Interview Questions and Answers

## 1. What are the key stages in the Physical Design flow?

The Physical Design flow consists of the following major stages:

- Floorplanning: Placement of macros, standard cells, and power planning.
- Placement: Arranging standard cells while optimizing timing and congestion.
- Clock Tree Synthesis (CTS): Creating a balanced clock network to minimize skew and insertion delay.
- Routing: Connecting all the components while meeting design rules.
- Signoff: Running static timing analysis (STA), power analysis, and DRC/LVS checks before tape-out.

---

## 2. What is the difference between pre-CTS and post-CTS placement?

- Pre-CTS placement: Cells are placed based on estimated timing without a clock tree.
- Post-CTS placement: Cells are optimized after the clock tree is built, improving timing and reducing clock skew.

---

## 3. What is the impact of congestion in physical design, and how is it resolved?

Congestion occurs when too many wires need routing in a limited area. It can cause routing failures, higher delay, and increased power consumption.

Ways to resolve congestion:

- Spread cells during placement.
- Use metal-layer routing optimally.
- Adjust macro placement and power planning.
- Enable cell padding and congestion-aware placement.

---

## 4. What is OCV (On-Chip Variation), and how does it affect timing?

OCV accounts for process variations across a chip, leading to timing uncertainty. It is modeled by:

- Setup analysis: Slow corner (max delay).
- Hold analysis: Fast corner (min delay).

OCV variations are mitigated using derating factors and advanced techniques like AOCV and POCV.

---

## 5. What is clock skew, and how is it minimized?

Clock skew is the difference in clock arrival times at different registers. It is minimized by:

- Balanced clock tree synthesis (CTS).
- Using clock buffers with matched delays.
- Using skew-aware placement and CTS constraints.

---

## 6. What are the different routing layers in an ASIC?

ASIC routing uses multiple metal layers:

- Lower metal layers (M1-M3): Local interconnects with high resistance.
- Mid-level metal layers (M4-M6): Used for signal routing.
- Higher metal layers (M7-M12): Used for power and global routing.

---

## 7. What is IR drop, and how is it analyzed?

IR drop occurs when there is voltage loss due to resistance in power delivery, affecting timing and functionality.

- Static IR drop: Average power consumption.
- Dynamic IR drop: Transient power fluctuations.

IR drop is mitigated by power grid optimization, decoupling capacitors, and thick metal layers.

---

## 8. What are antenna violations in physical design?

Antenna violations occur during metal etching, where long interconnects accumulate excess charge, potentially damaging transistors.

Ways to fix antenna violations:

- Insert diodes at sensitive gates.
- Break long nets using vias.

---

## 9. What is the difference between global and detailed routing?

- Global routing: Creates rough paths for signals and assigns layers.
- Detailed routing: Determines exact wire paths and assigns tracks.

---

## 10. What are the key objectives of floorplanning?

- Macro placement to optimize data flow.
- Power planning to avoid IR drop.
- Congestion minimization by strategic placement.
- Aspect ratio optimization for efficient layout.

---

## 11. How does congestion impact timing in physical design?

Congestion causes longer wire detours, increasing wire resistance, capacitance, and signal delay, leading to setup violations.

To fix congestion:

- Use congestion-aware placement and routing techniques.

---

## 12. What is metal density, and why is it important?

Metal density refers to the distribution of metal layers across the chip. It is important to:

- Avoid CMP (Chemical Mechanical Polishing) issues.
- Reduce variation in resistance and capacitance.
- Ensure uniform power distribution.

---

## 13. What is ECO (Engineering Change Order) in Physical Design?

ECO is a late-stage modification to the design without rerunning full synthesis. It is used to:

- Fix functional or timing issues.
- Optimize power or performance.
- Reduce area post-signoff.

---

## 14. What is the purpose of filler cells in Physical Design?

Filler cells are used to:

- Maintain continuity of N-well and P-well for power distribution.
- Ensure proper spacing between cells.
- Avoid DRC violations.

---

## 15. What is cross-talk in routing, and how is it reduced?

Crosstalk is unwanted interference between adjacent nets due to capacitive coupling.

Ways to reduce crosstalk:

- Increase spacing between critical nets.
- Use shielding (ground/power tracks).
- Route signals on different metal layers.

---

## 16. What is the impact of multi-cycle paths on timing analysis?

Multi-cycle paths require more than one clock cycle to propagate data. They:

- Relax setup timing constraints.
- Need careful exception handling in STA.

---

## 17. What are hold violations, and how do you fix them?

Hold violations occur when data propagates too quickly, causing incorrect latching.

Ways to fix hold violations:

- Insert small buffers to delay the signal.
- Adjust clock skew.

---

## 18. What is clock gating, and how does it improve power efficiency?

Clock gating disables the clock signal to inactive blocks, reducing dynamic power consumption.

- Implemented using clock gating cells.
- Controlled by enable signals.

---

## 19. What are the challenges in multi-power domain designs?

Multi-power domain designs use isolation cells, level shifters, and retention cells to handle:

- Voltage level mismatches.
- State retention during power gating.
- Complex power sequencing.

---

## 20. How does signoff verification ensure a tapeout-ready design?

Signoff verification includes:

- Static Timing Analysis (STA) to ensure timing closure.
- IR Drop Analysis to check power integrity.
- DRC/LVS Checks to ensure design rule compliance.
- Antenna Rule Check to prevent device damage.

---