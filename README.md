# MUPC: the Mostly Useless Programmable Calculator

MUPC is a small 8-bit hobby CPU. This repository contains the hardware design for [Logisim Evolution](https://github.com/logisim-evolution/logisim-evolution) and the architecture documentation.

## Links
 - [danielde8/mupc](https://github.com/danielde8/mupc) - Logisim Evolution CPU schematic (this repository)
 - [danielde8/mupc-asm](https://github.com/danielde8/mupc-asm) - Prototype assembler written in Kotlin
 - [danielde8/mupc-emu](https://github.com/danielde8/mupc-emu) - Prototype emulator written in C
 - [erikflorian/mupc-cc](https://github.com/erikflorian/mupc-cc) - C Compiler for MUPC; beware that this is mostly AI-generated and produces very inefficient binaries

## Instruction encoding

The byte layout is `OOOO RR SS`: `O` is the 4-bit opcode, and `R` and `S` are the two 2-bit fields. For the grouped opcodes below, the first field selects a sub-operation and the second field selects a register. Registers are encoded as A=`00`, B=`01`, C=`10`, and D=`11`.

| Opcode | Encoding / operation |
| --- | --- |
| `0000` | `MOV R,S` |
| `0001` | `ADD R,S` |
| `0010` | `SUB R,S` |
| `0011` | `AND R,S` |
| `0100` | `OR R,S` |
| `0101` | `XOR R,S` |
| `0110` | `SHR R,S` |
| `0111` | `00 INC S`; `01 DEC S`; `10 ADC S`; `11 SBC S` |
| `1000` | `00 JMP`; `01 JZ S`; `10 JNZ S`; `11 JC` |
| `1001` | `JE R,S` |
| `1010` | `JG R,S` |
| `1011` | `JL R,S` |
| `1100` | `00 RDM S`; `01 WRM S`; `10 POP S`; `11 PUSH S` |
| `1101` | `00 IN S`; `01 OUT S` (followed by a channel byte) |
| `1110` | `00 LDO S`; `01 RND S`; `10 SDW`; `11 RBT` |
| `1111` | `00 LDI S,imm`; `01 ADI S,imm` |

## Project status

The Logisim circuit is unfinished and still missing some major features, please use the emulator - [mupc-emu](https://github.com/danielde8/mupc-emu) - instead.