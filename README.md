# Pipeline Implementation of MIPS32 processor
This is the Capstone project of the course ["Hardware Modeling Using Verilog"](https://onlinecourses.nptel.ac.in/noc21_cs60/preview) by professor [Indranil Sen Gupta](http://www.facweb.iitkgp.ac.in/~isg/). I created a [wiki](https://github.com/stativeboss/MIPS32/wiki) that covers the basic theory for this project.

**This project was intended to give an insight into how we go about modeling various sub-modules such as a register banks, and implement pipelining in a processor. As an add-on (over and above what is covered in the course), I plan to use [SOFA](https://github.com/lnis-uofu/SOFA) to generate the timing, power, and utilization reports for the designed processor**. 


The [verilog code](https://github.com/stativeboss/MIPS32/blob/main/RTL/mips.v), the [test-bench](https://github.com/stativeboss/MIPS32/blob/main/RTL/mips_tb.v), and the [simulation results](https://github.com/stativeboss/MIPS32/tree/main/results) are included in this repo.

## Considerations
- There are 32 general purpose registers (R0 to R31 each 32-bit) out of which R0 is non-writeable and contains the value 0.
- Program Counter (PC) is a 32-bit special purpose register.
- No flag registers.
- Memory is word accessible and each word is of 32-bit.

## Instruction subset used
 * <details>
      <summary>Load and Store Instructions</summary>
  
      - LW R1, 20(R2) // Add 20 to the data in R2. The result is taken as an address and the data present in that memory address is stored in R1.
      - SW R1, -3(R2) // Mem [R2-3] = R1 meaning 3 is subtracted from the value in R2 and the content in R1 is stored in that memory address. 
      </details>
      
 * <details>
      <summary>Arithmetic and Logic instructions with only register operands</summary>
  
      - ADD R1, R2, R3 // Add data in R2 and R3 and store the result in R1
      - SUB R1, R2, R3 // Subtract the data in R3 from the data in R2 and store the result in R1
      - MUL R1, R2, R3 // Multiply the data in R2 and R3 and store the result in R1
      - AND R1, R2, R3 // Perform bit-wise AND operation of the data in R2 and R3 and store the result in R1
      - OR R1, R2, R3 // Perform bit-wise OR operation of the data in R2 and R3 and store the result in R1
      - SLT R1, R2, R3 // If the data in R2 is less than the data in R3, set R1 else R1 = 0
      </details>
      
 * <details>
      <summary>Arithmetic and Logic instructions with immediate operand</summary>
  
      - ADDI R1, R2, 2 // Add data in R2 and 2, and store the result in R1
      - SUBI R1, R2, 3 // Subtract 3 from the data in R2, and store the result in R1
      - SLTI R1, R2, 4 // If the data in R2 is less than 4, set R1 else R1 = 0
      </details>
 
 * <details>
      <summary>Branch Instructions</summary>
  
      - BEQZ R1, LABEL // Branch to LABEL if data in R1 is 0
      - BNEQZ R1, LABEL // Branch to LABEL if data in R1 is not 0
      </details>

 * <details>
      <summary>Miscellaneous Instructions</summary>
  
      - HLT // Halt
      </details>
      

## R-Type Instruction Encoding

![image](https://user-images.githubusercontent.com/14873110/172476834-9a5d6750-e088-4ef3-ade8-00d84c7a7943.png)

With 6-bits dedicated to the Opcode, we can represent 2^6 (i.e., 64) instructions. Since the instruction set that's implemented in this project is small, 6-bits are enough for the Opcode. The below table shows the R-Type instructions with their opcode:

     
| Instruction | opcode |
| :--: | :--: |
|ADD | 000000|
|SUB | 000001|
|AND | 000010|
|OR  | 000011|
|SLT | 000100|
|MUL | 000101|
|HLT | 111111|

So, if we have an instruction ```ADD R1, R2, R3``` , it'd be 000000 00011 00010 00001 00000 000000 which would in turn be 00620800h in Hexadecimal.

## I-Type Instruction Encoding

![image](https://user-images.githubusercontent.com/14873110/172482737-b29e2751-5d5e-4330-94cb-a3ac698d6eb5.png)

The following table shows the I-Type instructions used along with their opcode:
| Instruction | opcode |
| :--: | :--: |
|LW | 001000|
|SW | 001001|
|ADDI | 001010|
|SUBI | 001011|
|SLTI | 001100|
|BNEQZ | 001101|
|BEQZ | 001110|

