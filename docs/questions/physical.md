# Physical Design (PD) Interview Questions

## 1. What are the key steps in ASIC Physical Design?
- **Floorplanning**  
- **Power Planning**  
- **Placement & CTS (Clock Tree Synthesis)**  
- **Routing**  
- **Timing Closure & Signoff**

## 2. What is clock skew and how is it managed?
Clock skew is the **difference in clock arrival times** at different flip-flops. Managed using:
- **Clock Tree Synthesis (CTS)**
- **Buffering and Load Balancing**
- **Useful Skew Adjustment**

## 3. What is OCV (On-Chip Variation) and why does it matter?
OCV accounts for **process variations across the die**, affecting **timing closure**.

## 4. What is IR Drop and how is it reduced?
IR Drop is **voltage loss due to resistance in power rails**. Reduced by:
- **Adding Power Straps**
- **Using Proper Decap Cells**
- **Optimizing Routing Layers**
