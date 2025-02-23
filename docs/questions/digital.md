# Digital Design Interview Questions

## Subtopics:
- [Verilog Syntax Questions](digital/verilog-syntax.md)
- [Logic Design Questions](digital/logic-design.md)
- [Clocking, Clock Dividers, and Reset Questions](digital/clocking.md)
- [Clock Domain Crossing (CDC) Questions](digital/cdc.md)
- [Power-Related Questions](digital/power.md)
- [Digital Filter Questions (FIR, IIR and CIC)](digital/digital_filters.md)
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

## AXI Interview Questions and Answers

1. What are the key differences between AXI3 and AXI4?
AXI4 introduces key improvements over AXI3:
- AXI4 removes write interleaving, making write data ordering simpler.
- AXI4 introduces burst transactions up to 256 beats, while AXI3 allows only 16 beats.
- AXI4 removes locked transactions, which were present in AXI3.
- AXI4 supports a simplified, more efficient interface for high-speed transfers.
2. How do the AXI read and write channels work?
AXI has independent read and write channels:
- **Write Transaction**: Uses `AW` (address write), `W` (write data), and `B` (write response) channels.
- **Read Transaction**: Uses `AR` (address read) and `R` (read data) channels.
Each transaction is handshake-based using `VALID` and `READY` signals.
3. Explain the purpose of AWVALID, WVALID, BVALID, ARVALID, and RVALID signals in AXI.
- **AWVALID**: Indicates a valid write address.
- **WVALID**: Indicates valid write data.
- **BVALID**: Indicates a valid write response.
- **ARVALID**: Indicates a valid read address.
- **RVALID**: Indicates valid read data.
4. What are the different response types in AXI, and what do they indicate?
- `OKAY (00)`: Successful normal access.
- `EXOKAY (01)`: Exclusive access successful (for locked transactions in AXI3).
- `SLVERR (10)`: Slave error occurred.
- `DECERR (11)`: Decode error, meaning an invalid address was accessed.
5. How does AXI ensure data integrity in transfers?
- AXI ensures integrity via handshaking (`VALID` and `READY` signals).
- It supports ECC (Error Correction Code) in high-reliability applications.
- It uses response signals (`BRESP`, `RRESP`) to indicate errors.
6. What is the significance of AWREADY, WREADY, BREADY, ARREADY, and RREADY signals?
- **AWREADY**: Slave is ready to accept the write address.
- **WREADY**: Slave is ready to accept the write data.
- **BREADY**: Master is ready to accept the write response.
- **ARREADY**: Slave is ready to accept the read address.
- **RREADY**: Master is ready to accept the read data.
7. How does AXI handle out-of-order transactions?
- AXI supports out-of-order transactions using unique transaction IDs (`AxID`).
- The slave can return responses in a different order than received but must ensure responses for the same ID maintain order.
- Reordering logic in interconnects allows efficient pipelining.
8. What are AXI QoS (Quality of Service) signals, and how do they impact system performance?
- `AxQOS` (4-bit signal) allows assigning priority to transactions.
- Higher priority transactions can be serviced first in congestion scenarios.
- Useful for real-time applications like video streaming and networking.
9. How does AXI achieve pipelined transactions?
- AXI decouples the address, data, and response phases using independent channels.
- This allows multiple transactions to be active simultaneously, improving bandwidth utilization.
10. How does AXI manage back-to-back transactions?
- The master can issue back-to-back transactions without waiting for responses.
- Out-of-order transactions allow parallel processing, improving efficiency.
11. How does an AXI interconnect work?
- An AXI interconnect routes transactions between multiple masters and slaves.
- It handles arbitration, protocol conversion, and clock domain crossing.
12. What happens if two AXI masters try to access the same AXI slave simultaneously?
- The interconnect arbitrates between masters using fairness or priority-based schemes.
13. Explain the different arbitration schemes used in AXI.
- **Round-robin**: Equal priority among masters.
- **Fixed priority**: High-priority master always wins.
- **Dynamic arbitration**: Adjusts priority based on real-time traffic.
14. How would you design an AXI interconnect for multiple masters and slaves?
- Use an AXI crossbar switch to allow concurrent master-slave transactions.
- Implement arbitration to resolve conflicts.
15. What are the advantages of using an AXI crossbar?
- Allows simultaneous multiple transactions.
- Reduces contention compared to shared-bus architectures.
16. What are the different types of AXI bursts?
- **FIXED**: All addresses are the same.
- **INCR**: Sequentially increasing addresses.
- **WRAP**: Wraps around on boundary crossing.
17. How does AXI handle misaligned data accesses?
- Uses `WSTRB` signals to enable specific bytes in a word.
18. What happens if an AXI burst crosses a 4KB boundary?
- AXI does not allow bursts to cross 4KB boundaries to prevent address wrap issues.
19. How is the AxLEN signal used in burst transactions?
- Specifies the number of data beats (0-255 in AXI4).
20. How does AXI handle write strobes (WSTRB)?
- Specifies which bytes are valid in a write transaction.
21. How does AXI handle clock domain crossing?
- Uses synchronizers, FIFOs, or asynchronous bridges.
22. What is an AXI register slice, and when should it be used?
- Adds pipeline registers to improve timing closure.
23. How does AXI handle reset and initialization?
- Uses `ARESETn` to reset all channels synchronously.
24. How would you design an AXI bridge between different clock domains?
- Use FIFO-based CDC techniques.
25. What are the challenges in designing an AXI-to-APB or AXI-to-AHB bridge?
- Handling protocol differences in timing, burst types, and response mechanisms.
