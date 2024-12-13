Samuel-Kanaan
Below is my attempt at Exam 3 for ECE 287-D

Overview
This project involves creating the `ex4_wrapper.v` module, a Verilog implementation of a given C function. Designed for the DE1-SOC board, the project follows a modular approach with each functionality encapsulated in its own module. The main system uses a finite-state machine (FSM) to coordinate the execution of these modules, handling memory operations, computations, and control flow as described in the C code.

Purpose
The module:
1. Initializes memory with random values and specific constraints.
2. Executes operations like finding values in memory, swapping nibbles, and determining minimum values.
3. Replicates the logic of the provided C function in a structured Verilog format.

How It Works

Top-Level Wrapper (`ex4_wrapper`)
The `ex4_wrapper` serves as the controller for the system. It:
- Manages inputs like clock (`clk`), reset (`reset`), and start signals (`start`), as well as two 16-bit inputs (`in1`, `in2`).
- Outputs a `done` signal to indicate completion and a 16-bit result (`output1`).

State Machine
The module uses an FSM to manage the process, with the following states:
- IDLE: Waits for the `start` signal.
- INIT: Initializes memory and ensures address 5 is set to `42`.
- CALC_X: Computes the value of `x` using the `Memory instance count` module and adjusts it based on conditions.
- CALC_Y: Calculates `y` as the absolute value of `in2` using the `Abs module` and applies bounds.
- LOOP: Iterates over memory to perform operations like nibble swapping and result updates.
- DONE: Signals completion and outputs the result.

Submodules
Each submodule mirrors a specific functionality from the C code. The modules include:
1. Abs Module: Computes the absolute value of a signed 16-bit number.
2. Swap Module: Swaps the most and least significant nibbles of a 16-bit value.
3. Memory Initialization: Initializes memory with random values and sets address 5 to `42`.
4. Memory Instance Count: Counts occurrences of a specific value in memory.
5. Minimum Value Computation: Finds the smallest value among four inputs.
6. RNG (Random Number Generator): Generates random 16-bit values.

Process Workflow
1. Memory Initialization:
   - The `Memory Initialization` module fills memory with random values in two's complement format.
   - Address 5 is explicitly set to `42` as a checksum value.

2. Main Computation:
   - The FSM calculates `x` and `y` using the `Memory Instance Count` and `Abs Module`.
   - Iterates over memory using the `Swap Module` to perform nibble swapping and updating results.

3. Result Output:
   - The final result is stored in `output1`, and the `done` signal is set to indicate completion.
   - 
Testing and Validation
- Simulation:
  - Testbenches simulate each individual submodule and the full FSM.
  - Random and edge-case inputs ensure robust design.

- FPGA Deployment:
  - The design is synthesized and tested on the DE1-SOC board, running at a 50MHz clock.
  
Features and Benefits
- Modular Design: Each functionality is isolated for clarity and ease of debugging.
- FSM-Based Logic: Ensures structured control flow and adherence to the Verilog design constraints.
- Efficient Operations: Handles two's complement arithmetic and memory operations effectively.
- Submission-Ready: The design integrates all functionality into a single `ex4_wrapper.v` file, meeting project requirements.

Notes
- The FSM implements loops and conditionals in a synthesizable manner.
- Memory operations are compliant with single-port RAM constraints for FPGA compatibility.
- The design avoids inferred latches and adheres to synthesizable Verilog practices.

Conclusion
The `ex4_wrapper.v` module faithfully implements the provided C code using a modular and FSM-based approach. Tailored for FPGA deployment on the DE1-SOC board, the design is reliable, maintainable, and fully meets the project requirements.

