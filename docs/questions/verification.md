# ASIC Verification Interview Questions

## 1. What is constrained random verification?
Constrained random verification (CRV) is a **UVM methodology** where input vectors are randomly generated under constraints to improve test coverage.

## 2. What is functional coverage, and how is it different from code coverage?
- **Functional coverage** ensures that all **features** and scenarios are tested.  
- **Code coverage** checks if all **statements, branches, and FSM states** in RTL were exercised.

## 3. What are assertions in verification?
Assertions are **properties written in SVA (SystemVerilog Assertions)** to monitor and validate signal behavior during simulation.

## 4. What is a transaction in UVM?
A transaction is a **data object** that captures signal transfers, representing a single event in stimulus-response modeling.

## 5. How do you debug a failing test in simulation?
1. **Check waveform (VCD, FSDB)**
2. **Analyze log files** for assertion failures
3. **Use UVM debug tools (uvm_report, backtrace)**
4. **Enable finer-grained print logs**
