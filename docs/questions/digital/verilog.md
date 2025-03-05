# Verilog for ASIC Interviews

Many companies evaluate Verilog skills using onlinr platforms like CoderPad, Hackerrank, or online Verilog simulators. Interviewers focus on following areas:

- Implementing a synthesizable Verilog module from given specifications
- Fixing syntax and logical errors
- Understanding power, area, and timing constraints
- Following are the common Verilog codes evaluated
    - Combinational circuits such as multiplexers, adders, and encoders  
    - Finite state machine (FSM) design  
    - Writing parameterized RTL for reusability  
    - Handling clock domain crossings (CDC) and metastability  
    - Debugging simulation failures and timing violations  

Let's look at some common verilog questions

---

### Arbitration in Multi-Client Systems  

Arbiters control access to shared resources when multiple requestors compete for access. Two common arbitration methods are:

- **Priority Arbiter**: Grants access based on a fixed priority order.
- **Round Robin Arbiter**: Distributes access fairly by rotating the grant order.

Below are Verilog implementations for both.

### 1. Priority Arbiter (Fixed Priority)

A priority arbiter grants access to the highest-priority requestor first. The request with the lowest index (`req[0]`) has the highest priority, while `req[3]` has the lowest.

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
### Key Features
- Fixed priority scheme: The lowest-numbered request has the highest priority.
- Casez statement: Allows `?` (don't care) for flexibility in priority encoding.
- Simple implementation: Efficient and minimal hardware overhead.

### Use Cases
- Interrupt controllers where some interrupts are more critical.
- Memory access arbitration where certain clients have higher priority.

### 2. Round Robin Arbiter
A round robin arbiter ensures fairness by granting requests in cyclic order. It avoids starvation by rotating priority after each successful grant.

### Implementation
This design keeps track of the last granted request (`last_grant`) and rotates priority accordingly.


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
### Key Features
- Rotating priority: Ensures fair access to all clients.
- State tracking (`last_grant`): Maintains the last granted request and shifts priority.
- No starvation: Every request eventually gets served.

### Use Cases
- Shared bus arbitration (e.g., AMBA, Wishbone).
- Scheduling mechanisms in networking (e.g., time-division multiplexing).
- Fair allocation of resources among multiple processing cores.

### Comparison: Priority vs. Round Robin

| Feature               | Priority Arbiter | Round Robin Arbiter |
|----------------------|----------------|----------------|
| Fairness         | No, favors lower request numbers | Yes, rotates priority |
| Implementation   | Simple priority logic | Requires state tracking |
| Latency          | Fast response for high-priority requests | Uniform latency distribution |
| Use Case         | Real-time critical systems | Shared resource fairness |

---

