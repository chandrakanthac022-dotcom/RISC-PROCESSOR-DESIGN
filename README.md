The alu.v file implements the Arithmetic Logic Unit (ALU) of the processor. The ALU performs arithmetic and logical operations such as addition, subtraction, AND, OR, and XOR. During execution, the Control Unit sends an ALU select signal, and based on that signal the ALU performs the required operation. For example, if the instruction is ADD R1, R2, R3, the ALU adds the values stored in R2 and R3 and generates the output result.

2️⃣ control_unit.v

The control_unit.v file controls the complete processor operation. It decodes the instruction opcode and generates all necessary control signals required for execution. These control signals include RegWrite, MemRead, MemWrite, ALUSrc, and Branch signals. The Control Unit decides whether the processor should perform arithmetic operations, access memory, or update registers.

3️⃣ register_file.v

The register_file.v file stores processor registers and temporary data used during instruction execution. The register file contains multiple general-purpose registers such as R0 to R31. It supports reading two registers simultaneously and writing one result back into a register. During execution, operands are fetched from the register file and sent to the ALU.

4️⃣ instruction_memory.v

The instruction_memory.v file stores all processor instructions. The Program Counter sends the instruction address to this module, and the corresponding instruction is fetched and sent to the processor for execution. For example, when the Program Counter value is 0, the instruction stored at memory location 0 is fetched.

5️⃣ data_memory.v

The data_memory.v file handles memory read and write operations. It is mainly used for load (LW) and store (SW) instructions. During a store operation, data from a register is written into memory. During a load operation, data is read from memory and sent back to the register file.

6️⃣ program_counter.v

The program_counter.v file stores the address of the next instruction to be executed. After every instruction execution, the Program Counter updates the address to the next instruction location. Normally, the PC value increases by 4 because each instruction occupies 4 bytes.

Example:

PC = PC + 4
7️⃣ sign_extender.v

The sign_extender.v file converts smaller immediate values into 32-bit values. Immediate values used in instructions are smaller in size, so this module extends them into a full 32-bit format before sending them to the ALU.

8️⃣ mux.v

The mux.v file implements a Multiplexer (MUX). It selects one input among multiple inputs based on a select signal. In the processor datapath, the MUX is used to select between register data and immediate values for ALU operations.

9️⃣ top_module.v

The top_module.v file is the main integration module of the processor. It connects all processor blocks such as Program Counter, Instruction Memory, Register File, ALU, Data Memory, and Control Unit together. This file controls the overall datapath and signal flow inside the processor.

🔷 Testbench Folder (testbench/)
🔟 processor_tb.v

The processor_tb.v file is used for simulation and verification of the processor design. It generates clock and reset signals, applies test instructions, and monitors processor outputs during simulation. This file helps verify whether the processor is functioning correctly.

🔷 Waveform Folder (waveform/)
simulation_output.png

This file contains the waveform output generated during simulation. The waveform shows signals such as clock, Program Counter, ALU output, memory operations, and register values. It helps analyze processor timing and functionality.

🔷 Documentation Folder (docs/)
architecture_diagram.png

This file contains the block diagram of the RISC processor architecture. It visually explains how different modules are connected together and how data flows inside the processor.

⚙️ Processor Working Stages
1️⃣ Instruction Fetch (IF)

In this stage, the Program Counter sends the instruction address to Instruction Memory. The instruction stored at that address is fetched and sent to the processor.

Example:

Instruction = Memory[PC]
2️⃣ Instruction Decode (ID)

In this stage, the instruction opcode is decoded by the Control Unit. Control signals are generated, and the Register File provides operand values required for execution.

3️⃣ Execute (EX)

In this stage, the ALU performs arithmetic or logical operations based on the instruction type. For example, the ALU performs addition for an ADD instruction.

Example:

R1 = R2 + R3
4️⃣ Memory Access (MEM)

In this stage, the processor accesses Data Memory during load and store instructions. Data is either read from memory or written into memory.

5️⃣ Write Back (WB)

In this stage, the final result from the ALU or Data Memory is written back into the Register File for future operations.

📖 Supported Instructions
Instruction Type	Instructions
Arithmetic	ADD, SUB
Logical	AND, OR, XOR
Immediate	ADDI
Memory	LW, SW
Branch	BEQ
Jump	
