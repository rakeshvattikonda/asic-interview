# Synthesis & Static Timing Analysis (STA) Interview Questions

## 1. What is the difference between RTL and netlist?
- **RTL** is high-level, written in Verilog/VHDL.  
- **Netlist** is a gate-level representation after synthesis.

## 2. What are false paths and multi-cycle paths?
- **False Path**: A timing path that **never gets activated in real operation**.
- **Multi-Cycle Path (MCP)**: A path that has **more than one clock cycle** to complete.

## 3. What are setup and hold time violations?
- **Setup Violation**: Data is not stable before the clock edge.
- **Hold Violation**: Data changes too early after the clock edge.

## 4. What is clock gating and why is it used?
Clock gating reduces **dynamic power consumption** by **disabling the clock** when logic is inactive.

## 5. What is the role of PrimeTime in ASIC design?
PrimeTime (PT) is a **timing analysis tool** used for:
- **Setup/Hold Analysis**
- **Clock Tree Analysis**
- **Path Delay Debugging**
