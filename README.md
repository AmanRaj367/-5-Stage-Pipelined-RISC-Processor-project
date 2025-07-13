# -5-Stage-Pipelined-RISC-Processor-project


This project implements a **5-stage pipelined RISC-V processor** in Verilog HDL. It simulates a simplified version of a RISC-V CPU capable of executing a subset of RV32I instructions using structural and behavioral modules. The processor is tested with sample instruction memory and verified using Icarus Verilog and GTKWave.

---

##  Project Objective

To design, simulate, and test a **5-stage pipelined processor architecture** with basic RISC-V instruction support using Verilog HDL. The goal is to demonstrate:
- Modular design using reusable components (ALU, control unit, register file, etc.)
- Instruction-level pipelining
- Clocked synchronous operation with instruction memory and register updates
- Simulation-based verification using GTKWave

---

##  Architecture Overview

The processor implements the following pipeline stages:

1. **IF – Instruction Fetch**  
   - Fetches instruction from instruction memory using PC

2. **ID – Instruction Decode / Register Fetch**  
   - Decodes instruction and reads registers from register file

3. **EX – Execute**  
   - Performs ALU operations and computes branch addresses

4. **MEM – Memory Access** *(optional extension)*  
   - Loads/stores data (not implemented in base version)

5. **WB – Write Back**  
   - Writes result back to the register file

---

## File Structure

```txt
├── alu.v                 # ALU logic
├── alu_control.v         # Generates ALU control signals
├── control_unit.v        # Decodes instruction and generates control signals
├── imm_generator.v       # Extracts and sign-extends immediates
├── instruction_memory.v  # ROM-based instruction memory
├── instructions.mem      # Hex file with sample instructions
├── register_file.v       # Register file with read/write support
├── riscv_top.v           # Top-level integration (pipeline stages)
├── riscv_top_tb.v        # Testbench for simulation
├── riscywave.vcd         # Waveform output from simulation
└── README.md             # You are here
```
---

##  Simulation Guide
##  Requirements
- Icarus Verilog
- GTKWave

###  Steps to Simulate
1. Compile the Verilog code:
```bash
iverilog -o riscv_test *.v
```
2. Run the simulation:
```bash
vvp riscv_test
```
3. View waveforms:
```bash
gtkwave riscywave.vcd
```

---

##  Sample Output on Terminal
```=== Instruction Execution Trace ===
Time: 10ns | PC: 00000000 | Instr: 00a00093 | rd: x1 | wb_data: 10
Time: 15ns | PC: 00000004 | Instr: 01400113 | rd: x2 | wb_data: 20
Time: 25ns | PC: 00000008 | Instr: 01e00193 | rd: x3 | wb_data: 30
Time: 35ns | PC: 0000000c | Instr: 003081b3 | rd: x3 | wb_data: 40
Time: 45ns | PC: 00000010 | Instr: 40210233 | rd: x4 | wb_data: 0
==== Register File Dump After Execution ====        
x0  = 0
x1  = 10
x2  = 20
x3  = 40
x4  = 0
```
