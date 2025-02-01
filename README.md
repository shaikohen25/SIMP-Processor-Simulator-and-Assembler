# SIMP-Processor-Simulator-and-Assembler

## Overview
This project implements a simulator and assembler for the SIMP processor, a simplified RISC processor similar to MIPS. The simulator executes SIMP machine code, and the assembler translates assembly instructions into machine code.

## Project Structure
- **asm.c**: The assembler that converts assembly code (`.asm` files) into machine code (`memin.txt`).
- **sim.c**: The simulator that executes machine code, producing various output files.
- **memin.txt**: Input file containing the machine code for the simulator.
- **Output Files**:
  - `memout.txt`: Final memory state after execution.
  - `regout.txt`: Final values of registers R2-R15.
  - `trace.txt`: Execution trace with register states.
  - `cycles.txt`: Total clock cycles used.

## Assembler (asm.c)
### Functionality:
- Reads an assembly file (`.asm`).
- Supports labels and translates them into addresses (two-pass approach).
- Converts instructions into binary machine code.
- Writes the machine code into `memin.txt`.

### Key Features:
- Supports instruction format parsing.
- Replaces labels with their corresponding memory addresses.
- Handles `.word` directives for direct memory initialization.

## Simulator (sim.c)
### Functionality:
- Reads `memin.txt` and initializes memory.
- Implements a **fetch-decode-execute loop**.
- Executes supported instructions:
  - Arithmetic (`add`, `sub`, `mul`)
  - Logical (`and`, `or`, `xor`)
  - Shifts (`sll`, `srl`, `sra`)
  - Branching (`beq`, `bne`, `blt`, `bgt`, `ble`, `bge`, `jal`)
  - Memory operations (`lw`, `sw`)
  - Halt (`halt`)
- Updates registers and memory accordingly.
- Tracks and writes execution details to output files.

### Key Features:
- Proper PC updates based on instruction type (R/I format).
- Handles memory and register operations efficiently.
- Outputs full execution trace.

## Compilation & Execution
### Compile:
```
gcc -o asm asm.c
gcc -o sim sim.c
```

### Run Assembler:
```
./asm program.asm memin.txt
```

### Run Simulator:
```
./sim memin.txt memout.txt regout.txt trace.txt cycles.txt
```

## Example
### Sample Assembly (`program.asm`):
```
add $t1, $zero, $imm, 5  # t1 = 5
add $t2, $t1, $imm, 3    # t2 = 8
halt $zero, $zero, $zero, 0
```
### Expected `memin.txt`:
```
000A0
001A3
3FFFF
```
### Expected `regout.txt` (Final Register Values):
```
00000000
00000000
00000000
00000005
00000008
...
```

## Notes
- Ensure `memin.txt` follows the correct format.
- The simulator stops execution when it encounters a `halt` instruction.
- Make sure to handle labels correctly in the assembler.

