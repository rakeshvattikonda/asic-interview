# AHB Interview Questions

This page contains **interview questions** related to the **AHB (Advanced High-performance Bus)** from the AMBA protocol.

---

## 1. What is the AMBA AHB protocol, and how does it differ from other AMBA protocols like APB and AXI?
AHB is a high-speed pipelined bus designed for efficient data transfers between system components.  

- **Differences from APB**: AHB is used for high-speed memory and peripherals, while APB is for low-speed peripherals (e.g., GPIO, UART).  
- **Differences from AXI**: AXI supports multiple outstanding transactions and out-of-order execution, while AHB follows a simpler single-address, single-data phase protocol.

---

## 2. Describe the various versions of AHB and their key differences.
- **AMBA 2 AHB**: Supports multiple masters and slaves.  
- **AHB-Lite**: A simplified version of AHB, designed for single-master systems (no arbitration).  
- **AHB5**: Adds TrustZone security and exclusive access support.

---

## 3. What are the primary advantages of AHB over other bus protocols in an SoC?
- **Higher performance**: Supports burst transfers and pipelining.  
- **Multiple masters**: Arbitration allows multiple bus masters.  
- **Efficient data transfer**: Supports 8-bit, 16-bit, and 32-bit transfers.  
- **Low-latency**: Split and retry responses improve slave performance.

---

## 4. What is the purpose of the AHB Bus Matrix, and how does it improve system performance?
The **AHB Bus Matrix** allows multiple masters to communicate with multiple slaves **simultaneously**. It improves performance by:
- **Reducing contention**: Masters can access different slaves at the same time.
- **Optimizing arbitration**: Implements **priority-based bus arbitration**.
- **Minimizing bottlenecks**: Enables **parallel transactions** instead of a single shared bus.

---

## 5. Explain the role of the following AHB signals: `HCLK`, `HRESETn`, `HADDR`, `HTRANS`, `HWRITE`, `HSIZE`.
- `HCLK`: Clock signal.  
- `HRESETn`: Active-low reset signal.  
- `HADDR`: Address bus (32-bit).  
- `HTRANS`: Transfer type (`IDLE`, `BUSY`, `NONSEQ`, `SEQ`).  
- `HWRITE`: `1` = Write, `0` = Read.  
- `HSIZE`: Transfer size (`8-bit`, `16-bit`, `32-bit`).

---

## 6. What is the function of the `HREADY` and `HREADYOUT` signals?
- `HREADY` (input) **tells the master** if the slave is ready for the next transaction.
- `HREADYOUT` (output) **indicates if the slave is ready**.

If `HREADY = 0`, the master must wait before sending the next request.

---

## 7. How does `HSEL` (Slave Select) work in AHB transactions?
- **AHB decoder asserts `HSEL`** to select the corresponding slave.  
- Only **one slave can be active at a time** for a given transaction.

---

## 8. What is the purpose of the `HBURST` signal, and how does it optimize transfers?
`HBURST` defines the **burst transaction type**:
- **SINGLE**: One transfer.
- **INCR**: Incrementing burst (no fixed length).
- **WRAP4, INCR4, WRAP8, INCR8, WRAP16, INCR16**: Fixed-length bursts.

**Optimization**: Burst transactions reduce **address overhead**, improving efficiency.

---

## 9. Explain the difference between address phase and data phase in an AHB transaction.
- **Address phase**: The master sends **HADDR, HTRANS, HWRITE, HSIZE**.  
- **Data phase**: The actual data transfer occurs **one cycle later**.

---

## 10. What is the role of the default slave, and what happens when an invalid address is accessed?
- The **default slave** is selected when no valid slave is assigned to the address.
- It returns an **ERROR response**, preventing undefined behavior.

---

## 11. How does an AHB slave indicate readiness for a new transfer?
- By asserting **HREADYOUT = 1**, meaning it has completed processing.
- If **HREADYOUT = 0**, the master must wait.

---

## 12. What is the impact of pipelined operations in AHB?
- **Pipelining overlaps address and data phases**.
- While one transfer is in the data phase, the next transfer's address phase begins.
- This improves **throughput and efficiency**.

---

## 13. How does multi-master arbitration work in AHB?
- **AHB arbiter** resolves conflicts when multiple masters request access.
- Key arbitration signals:
  - `HGRANT`: Grants bus ownership.
  - `HLOCK`: Indicates locked transactions.
  - `HMASTER`: Shows current master.
- Uses **priority-based or round-robin arbitration**.

---

## 14. What changes were introduced in AHB-Lite?
- **AHB-Lite is a single-master version of AHB** (no arbitration).
- It **removes unnecessary logic**, making it **ideal for simple SoCs**.

---

## 15. How does AHB5 support exclusive access and TrustZone?
- **Exclusive access** ensures **atomic read-modify-write** operations.
- **TrustZone uses `HNONSEC` signal** to separate **secure and non-secure transactions**.

---

## 16. What is a burst transaction, and why is it useful?
A **burst transaction** is a sequence of **back-to-back transfers** using a single **address phase** to reduce overhead.

---

## 17. What is the difference between incrementing and wrapping bursts?
- **Incrementing (INCR)**: Address **increases sequentially**.
- **Wrapping (WRAP)**: Address **wraps around at boundaries** (e.g., `4-beat burst at 0x10, 0x14, 0x18, wraps to 0x00`).

---

## 18. How does a slave handle an incomplete burst transaction?
- It can **terminate with an ERROR response**, forcing the master to retry or handle the error.

---

## 19. What happens if a slave does not support bursts?
- The slave **treats all transfers as SINGLE** and ignores the `HBURST` signal.

---

## 20. How do burst transactions improve DRAM access efficiency?
- **Sequential bursts** maximize **row buffer hits** in DRAM.  
- **Avoids row activation overhead**, improving memory bandwidth.

---