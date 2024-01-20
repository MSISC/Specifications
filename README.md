# Specifications

## Instruction Parameter Types
| Parameter Type| Description |
|-----------------------|--------|
| imm8 | An immediate value (a constant value baked into the code at compile time). Usually present in the byte after the opcode|
| mem8 | A type of immediate value used as a memory address in the lda and sto instructions with no structural difference | 
| reg8 | A register number, usually added to the base opcode value to differentiate between similar instructions with use or store values to different registers. The register numbers for the 4 general purpose registers are given below.|

## Instructions
| Byte 0 (Opcode) | Byte 1 | Instruction | Description |
|-----------------------|--------|--------|-------------|
|00-03|00-FF| sto &lt;mem8&gt;, &lt;reg8&gt; | Stores data in register to memory location |
|04-07|00-FF| lda &lt;reg8&gt;, &lt;mem8&gt; | Loads data into register from memory location |
|08-0B|| jmprel &lt;reg8&gt; | Jumps a certain number of bytes ahead from the start of this instruction |
|0C|00-FF| jmprel &lt;imm8&gt; | Jumps a certain number of bytes ahead from the start of this instruction |
|0E|00-FF| mul &lt;imm8&gt; | Multiplies register A by a value |
|0F|00-FF| add &lt;imm8&gt; | Adds a value to register A |
|0F|00-FF| sub &lt;imm8&gt; | Subtracts a value from register A |
|10-13|| mul &lt;reg8&gt; | Multiplies register A by a value |
|14-17|| add &lt;reg8&gt; | Adds a value to register A | 
|18-2B|| sub &lt;reg8&gt; | Subtracts a value from register A |
|2C-2F|| imul &lt;reg8&gt; | Signed multiplies register A by a value |
|30-33|| iadd &lt;reg8&gt; | Signed adds register A by a value |
|34-37|| neg &lt;reg8&gt; | Negates a value and stores in A |
|38|00-FF| imul &lt;imm8&gt; | Signed multiplies register A by a value |
|39|00-FF| iadd &lt;imm8&gt; | Signed adds register A by a value |
|3B|00-FF| jmpfar &lt;imm8&gt; | Jumps to an absolute address |
|3C-3F|| cmp &lt;reg8&gt; | Compares register A to value and stores in flags |
|40|00-FF| cmp &lt;imm8&gt; | Compares register A to value and stores in flags |
|41|00-FF| or &lt;imm8&gt; | ORs register B with value and stores in register B |
|42|| nop | No Operation |
|43|00-FF| and &lt;imm8&gt; | ANDs register B with value and stores in register B |
|44+bitmap|00-FF| jmprel &lt;imm8&gt; | Jumps a certain number of bytes ahead if bmap AND flags != 0 (bitmap in instruction itself and imm8 in byte after opcode). |
|4C-4F|00-07| jmprel &lt;reg8&gt; | Jumps a certain number of bytes ahead if bmap AND flags != 0  (reg8 in instruction itself and bitmap in byte after opcode).  |
|50-53|00-FF| or &lt;reg8&gt; | ORs register B with value and stores in register B |
|54-57|00-FF| and &lt;reg8&gt; | ANDs register B with value and stores in register B |
|58|00-0F| mov &lt;reg8&gt;, &lt;reg8&gt; | Moves value from first reg8 into second reg8. (higher 2 bits are register A and lower 2 bits are register B) |
|59|| out | Outputs data into port in register A with value in register B |
|5A|| in | Inputs data from port in register A into register B |
|5B|00-01| features &lt;imm8&gt; | Returns the feature byte at a certain byte no. (given below) into register C |
|5C-5F|00-FF| mov &lt;reg8&gt;, &lt;imm8&gt; | Moves value into given register |
|60-63|| features &lt;reg8&gt; | Returns the feature byte at a certain byte no. (given below) into register C |
|64|| clf | Clears the flags register |
|65|| nf | Negates the flags register |
|66|| gf | Stores the flags register in register D |
|68-7B|| not &lt;reg8&gt; | Bitwise NOT's a value and stores in B |

## Flags
| Bit No | Name | Description |
|---|---|---|
| 0 | Equal | The values are equal | 
| 1 | Less | Value A &lt; Value B |
| 2 | Greater | Values B &lt; Value A |

## Registers:
| Register No | Name | Description |
|---|---|--|
|0| A | general purpose register used in math operations |
|1| B | general purpose register used in bitwise operations |
|2| C | general purpose register used for features operation |
|3| D | general purpose register used to interface with the flags register |
|4| PC | program counter, edited using jmp* instructions |
|5| FLAGS | flags register, edited using cmp instructions |

## List of Feature Attributes:
### Byte 0:
8 bit CPU version (currently v0)


### Byte 1:
| Bit No | Description |
|---|---|
| 0 | 16-bit supported | 
| 1 | 32-bit supported | 
| 2 | 64-bit supported | 
| 3-7 | Unused |

## Architectural Limits
- 8 bit wide address lane
- Maximum memory size of 256 (can be circumvented by interfacing with an external memory module)
- 256 IO ports
- Currently 4 general purpose registers

  








