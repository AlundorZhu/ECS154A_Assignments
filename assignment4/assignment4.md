# Building a single bus 8-bit CPU (Working Progress)
![CPU](CPU.png)
## You will be building a cpu with the following specifications:

**Hint** use this [example](genericcpu.pdf) from class as a guide.

The RAM content is provided in [RAMcontent](RAMcontent) file. (Not ready yet) It will contain both instructions and data.

We are going to show from beginning to end how to wire up a generic 8-bit machine.  This machine will use a 2-operand format, meaning that instructions are of the time A=A+B.  So, for example, "Add r0, r1" is r0=r0+r1.

The machine is byte-addressable.  Offsets are sign-extended, and jumps are done by adding the sign-extended offset field to the PC.  Immediates are not sign-extended.

## The machine has 3 different instruction formats:  A, B, and C.

A-type: 
| Opcode |  ds  |   s   | extra |
|--------|------|-------|-------|
| 7-4    |  3   |   2   | 1-0   |


B-type: 
| Opcode |  ds  |   Immediate   |
|--------|------|---------------|
| 7-4    |  3   |     2-0       |

C-type: 
| Opcode |  Offset   |
|--------|-----------|
| 7-4    |   3-0     |

## The ALU can perform 4 functions:

| Operation       | ALU0    | ALU1    |
|-----------------|---------|---------|
| Add             | 1       | 1       |
| Sub             | 1       | 0       |
| Mult            | 0       | 1       |
| Nand            | 0       | 0       |

## Here are a few of the instructions that have been defined:
| Instruction Format | Opcode | Operation |
|--------------------|--------|-----------|
| nand               | 0000   | rds=~(rds & rs) |
| add                | 0001   | rds=rds+rs |
| addm               | 0010   | rds=rds+mem[rs] |
| addi               | 0011   | rds=rds+imm |
| sub                | 0100   | rds=rds-rs |
| addmi              | 0110   | rds=rds+mem[rs+imm] |
| jmp                | 1111   | PC=PC+offset (offset is sign extended) |

## You will need to expose the following registers for autograding purposes: (Working Progress)
- R0
- R1