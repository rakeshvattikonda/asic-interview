# Clock Domain Crossing (CDC) Analysis - Interview Questions and Answers

## 1. What is Clock Domain Crossing (CDC)?

Clock Domain Crossing (CDC) occurs when a signal is transferred from one clock domain to another. This can lead to metastability, data loss, or incorrect timing if not handled properly.

---

## 2. Why is CDC analysis important in ASIC design?

- Ensures data integrity when signals cross different clock domains.
- Detects potential metastability issues.
- Helps avoid setup and hold time violations.
- Prevents glitches due to asynchronous transitions.

---

## 3. What are the common issues faced in CDC?

- Metastability due to unsynchronized signals.
- Data loss if a signal is sampled incorrectly.
- Glitches due to asynchronous control signals.
- Setup and hold violations in fast-changing signals.

---

## 4. What are the common synchronization techniques for CDC?

- Two-flop synchronizer for single-bit signals.
- Handshake-based synchronization for control signals.
- FIFO-based synchronization for data transfers.
- Gray code for multi-bit control signals.

---

## 5. How does a two-flop synchronizer help in CDC?

- Reduces metastability by allowing the signal to settle over two clock cycles.
- Ensures a stable output in the receiving domain.
- Works well for single-bit signals.

---

## 6. What are the limitations of a two-flop synchronizer?

- Cannot handle multi-bit signals due to different arrival times of bits.
- Not suitable for fast-changing control signals or large data buses.
- Does not provide acknowledgment or handshaking.

---

## 7. What is metastability, and how does it occur in CDC?

Metastability occurs when a signal transition violates setup or hold time, causing the flip-flop to enter an unpredictable state. It typically happens when data is transferred between unrelated clock domains.

---

## 8. What is the role of a handshake synchronizer?

- Ensures safe data transfer between different clock domains.
- Uses request-acknowledge protocol to confirm data reception.
- Prevents data loss and metastability.

---

## 9. When should a FIFO be used for CDC?

- When transferring large amounts of data across clock domains.
- When source and destination clocks have different frequencies.
- When the data transfer requires buffering.

---

## 10. How does a CDC FIFO work?

- The write side operates in the source clock domain.
- The read side operates in the destination clock domain.
- Read and write pointers are synchronized using Gray coding or dual-clock pointers.

---

## 11. What are Gray codes, and why are they used in CDC?

- Gray codes change only one bit at a time, avoiding glitches.
- They are used for FIFO read/write pointers to ensure safe synchronization.
- Prevents erroneous data sampling in asynchronous domains.

---

## 12. What are the challenges in handling multi-bit CDC signals?

- Each bit may experience different metastability effects.
- Timing mismatches can cause incorrect data sampling.
- Requires encoding techniques like Gray coding or handshake synchronization.

---

## 13. What are clock-domain crossing violations in Static Timing Analysis (STA)?

- CDC paths are often asynchronous, so STA cannot analyze them directly.
- Setup and hold time violations occur if timing is not properly constrained.
- Special constraints or simulation-based verification is required.

---

## 14. What is reconvergence in CDC, and why is it problematic?

- Reconvergence occurs when multiple unsynchronized signals are combined before reaching a common logic.
- It can lead to glitches and incorrect circuit behavior.
- Proper synchronization and CDC-aware design techniques are needed to prevent it.

---

## 15. What is the purpose of CDC verification tools?

CDC verification tools:
- Identify potential metastability issues.
- Detect missing or incorrect synchronizers.
- Analyze different clock frequencies and data transfer protocols.
- Help ensure CDC paths are safely handled.

---

## 16. How is CDC analysis performed in simulation?

- Functional simulations cannot detect metastability accurately.
- CDC-aware simulations use metastability models.
- Formal verification or dynamic CDC simulations are used to check data integrity.

---

## 17. What is asynchronous reset de-assertion, and how is it handled?

- When a reset signal is released asynchronously, different flip-flops may deassert at different times.
- Can cause unpredictable circuit behavior.
- Proper reset synchronization ensures a clean and reliable de-assertion.

---

## 18. What is a pulse synchronizer, and where is it used?

- Converts a single-cycle pulse from one clock domain to another.
- Ensures safe pulse detection without missing or duplicating pulses.
- Commonly used in control signal synchronization.

---

## 19. How do you constrain CDC paths in SDC constraints?

- CDC paths are marked as false paths in STA.
- Constraints are added to handle proper synchronization.
- Proper clock groups and asynchronous path exceptions are defined.

---

## 20. How do you debug CDC-related failures in silicon?

- Use on-chip probes to monitor CDC signals.
- Check if proper synchronizers are implemented.
- Perform post-silicon timing analysis to detect violations.
- Measure metastability effects under different conditions.

---