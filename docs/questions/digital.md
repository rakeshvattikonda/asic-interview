# Digital Design Interview Questions

## Subtopics:
- [Verilog Syntax Questions](digital/verilog-syntax.md)
- [Logic Design Questions](digital/logic-design.md)
- [Clocking, Clock Dividers, and Reset Questions](digital/clocking.md)
- [Clock Domain Crossing (CDC) Questions](digital/cdc.md)
- [Power-Related Questions](digital/power.md)
- [Digital Filter Questions (FIR, IIR and CIC)](digital/digital-filters.md)
## 1. What is setup and hold time?
Setup time is the minimum time **before** the clock edge that data must be stable.  
Hold time is the minimum time **after** the clock edge that data must remain stable.

## 2. What happens if setup time is violated?
A setup time violation can cause **metastability**, leading to unpredictable output states.

## 3. How does a flip-flop differ from a latch?
| Feature     | Flip-Flop (FF) | Latch |
|------------|--------------|-------|
| Triggered by | Clock edge | Level-sensitive |
| Power Consumption | Higher | Lower |
| Usage | Registers, Pipelines | Gating, Low-power designs |

## 4. How do you synchronize an asynchronous signal in a clocked system?
A **2-flop synchronizer** is used to avoid metastability when transferring signals across clock domains.

## 5. What is meant by "glitch" in combinational logic?
A glitch is a **temporary unintended pulse** due to differing propagation delays in logic paths.

