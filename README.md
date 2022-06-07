# Pipeline Implementation of MIPS32 processor with reduced instruction set
This is the Capstone project of the course ["Hardware Modeling Using Verilog"](https://onlinecourses.nptel.ac.in/noc21_cs60/preview) by professor [Indranil Sen Gupta](http://www.facweb.iitkgp.ac.in/~isg/). I created a [wiki](https://github.com/stativeboss/MIPS32/wiki) that covers the basic theory for this project.

**This project was intended to give an insight into how we go about modeling various sub-modules such as a register banks, and implement pipelining in a processor. As an add-on, I used [SOFA](https://github.com/lnis-uofu/SOFA) to generate the timing, power, and utilization reports for the designed processor**. 


The verilog code, the test-bench, and the simulation results are included in this repo.

## Considerations
- There are 32 general purpose registers (R0 to R31 each 32-bit) out of which R0 is non-writeable and contains the value 0.
- Program Counter (PC) is a 32-bit special purpose register.
- No flag registers.
- Memory is word accessible and each word is of 32-bit.

## Instruction subset used
  - <details>
      <summary>Load and Store Instructions</summary>
      - LW R1, 20(R2) // Add 20 to the data in R2. The result is taken as an address and the data present in that memory address is stored in R1.
      - SW R1, -3(R2) // Mem [R2-3] = R1 meaning 3 is subtracted from the value in R2 and the content in R1 is stored in that memory address. 
      </details>
      
