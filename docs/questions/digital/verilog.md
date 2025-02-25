# Verilog for ASIC Interviews

## Why is Verilog Important in Interviews?

Verilog is a fundamental hardware description language (HDL) used in ASIC and FPGA design. It plays a key role in designing, verifying, and implementing digital circuits. Strong Verilog coding skills are essential for ASIC engineers, and many companies test candidates' abilities in:

- Writing synthesizable RTL for real-world ASIC designs.
- Debugging and analyzing Verilog simulations.
- Implementing common digital circuits, such as state machines, multiplexers, FIFOs, and memory controllers.
- Understanding power, area, and timing constraints during synthesis.

## Real-Time Coding in Interviews

Many companies use CoderPad, Hackerrank, or online Verilog compilers during interviews to evaluate coding skills. Candidates are often required to:

- Implement a Verilog module based on given specifications.
- Fix syntax or logical errors in a Verilog snippet.
- Write testbenches to verify functionality.
- Understand synthesizability and timing constraints.

### Common Verilog Tasks in Live Interviews:
- Implementing combinational circuits (multiplexers, adders, encoders).
- Designing finite state machines (FSMs).
- Writing parameterized RTL for reusability.
- Handling clock domain crossings (CDC) and metastability.
- Debugging failing simulations and timing violations.

---

# Verilog Coding Examples

## 4-bit Arbiter: Priority and Round Robin

Arbiters are essential in multi-client communication systems where multiple requestors compete for a shared resource. Two common arbitration mechanisms are:

- **Priority Arbiter**: Grants access based on a fixed priority order.
- **Round Robin Arbiter**: Ensures fairness by rotating the grant order among requestors.

Below are the Verilog implementations for both.


## 1. Priority Arbiter (Fixed Priority)
A **priority arbiter** grants access to the highest-priority requestor first. The request with the lowest index (`req[0]`) has the highest priority, while `req[3]` has the lowest.

### Implementation
The design uses a case statement to check requests in priority order, granting access to the first active request.

```verilog 
module priority_arbiter(
    input logic clk, rst,
    input logic [3:0] req,  // Request signals from 4 clients
    output logic [3:0] grant  // Grant signal to one client
);
    always_ff @(posedge clk or posedge rst) begin
        if (rst)
            grant <= 4'b0000;
        else begin
            casez (req)
                4'b1??? : grant <= 4'b1000; // Highest priority (req[3])
                4'b01?? : grant <= 4'b0100; // Second highest (req[2])
                4'b001? : grant <= 4'b0010; // Third highest (req[1])
                4'b0001 : grant <= 4'b0001; // Lowest priority (req[0])
                default : grant <= 4'b0000; // No request
            endcase
        end
    end
endmodule
```
```verilog 
module round_robin_arbiter(
    input logic clk, rst,
    input logic [3:0] req,  // Request signals from 4 clients
    output logic [3:0] grant  // Grant signal to one client
);
    logic [1:0] last_grant; // Stores last granted request

    always_ff @(posedge clk or posedge rst) begin
        if (rst)
            last_grant <= 2'b00; // Reset to first client
        else if (|req) begin  // If any request is active
            case (last_grant)
                2'b00: grant <= (req[1]) ? 4'b0010 : 
                                (req[2]) ? 4'b0100 : 
                                (req[3]) ? 4'b1000 : 
                                (req[0]) ? 4'b0001 : 4'b0000;
                2'b01: grant <= (req[2]) ? 4'b0100 : 
                                (req[3]) ? 4'b1000 : 
                                (req[0]) ? 4'b0001 : 
                                (req[1]) ? 4'b0010 : 4'b0000;
                2'b10: grant <= (req[3]) ? 4'b1000 : 
                                (req[0]) ? 4'b0001 : 
                                (req[1]) ? 4'b0010 : 
                                (req[2]) ? 4'b0100 : 4'b0000;
                2'b11: grant <= (req[0]) ? 4'b0001 : 
                                (req[1]) ? 4'b0010 : 
                                (req[2]) ? 4'b0100 : 
                                (req[3]) ? 4'b1000 : 4'b0000;
            endcase
        end else
            grant <= 4'b0000;
    end

    always_ff @(posedge clk or posedge rst) begin
        if (rst)
            last_grant <= 2'b00;
        else if (|grant) begin
            case (grant)
                4'b0001: last_grant <= 2'b00;
                4'b0010: last_grant <= 2'b01;
                4'b0100: last_grant <= 2'b10;
                4'b1000: last_grant <= 2'b11;
            endcase
        end
    end
endmodule
```
