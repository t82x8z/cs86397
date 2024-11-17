java c
EECS 370 Final Exam
Winter 2021
Question 1: Short Question Multiple Choice
[11 points - 1pt per question. Honor code + 10 were given]
1.  Honor Code Signature
2.  Having a pipeline with more stages will (always/sometimes/never) decrease the overall execution time.
3.  Given the same set of instructions, a pipeline that uses detect and stall will
sometimes perform. better than a pipeline that uses detect and forward with speculate and squash. Assume both pipelines have the same clock period and are identical in every way except how hazards are handled. (True/False)
4.  A pipeline that uses speculate and squash to handle control hazards could have
0 squashes if all branches are predicted correctly. (True/False)
5.  Caches are an important part of computers because they generally store more memory relative to the hard disk and have very little latency. (True/False).
6.  A fully associative cache will (always/sometimes/never) require more tag bits per entry as the cache size gets larger, given that all cache sizes are powers of 2.
7.  A write-through cache system will (always/sometimes/never) write to both cache and memory.
8.  A cache with very large block sizes will generally have less compulsory misses than a cache with smaller block sizes. (True/False)
9.  SRAM will have higher costs to make but will generally also have higher latency compared to DRAM and the disk. (True/False)
10. The TLB lookup could happen in the pipeline after the virtual address is calculated and before the memory reference is executed. (True/False)
11. The translation look-aside buffer will often have a hit rate that is greater than 90%. (True/False)
12. The number of instructions will (increase/stay the same/decrease) in a detect and stall pipeline if data and control hazards are present.
13. Caches are generally an (SRAM/DRAM) device.
14. Implementing spatial locality in a cache will result in less cache misses than
implementing temporal locality when accessing every element only once in the array incrementally. (True/False)
15.A direct mapped cache will only check (a) (single/multiple/all) tag(s) to see if it matches with the required memory address.
16. The total size of a multi level page table could be greater than the size of a single level page table. (True/False)
Question 2: Detecting Hazards in LC2K Code (Version 1) [12 points]
Suppose the following LC2K assembly code is run through the 5-stage pipeline from lecture until it halts.

1. Select all registers that cause a RAW (Read after write) data hazard in a
detect and stall pipeline. Assume that data hazards are resolved with detect     and stall. Assume that control hazards are resolved with detect and stall. Data hazards can only occur from instructions that are executed. [3 pts]a.  reg0 b.  reg1 c.  reg2 d.  reg3 e.  reg4 f.   reg5 g.  reg6 h.  reg7
2.  Using detect and stall to resolve data hazards, and detect and stall to
haza(reso)lrd(ve)sc?o[3(n)t pt(ro)lsh]azards, what is the number of stalls that occur only due to data3. Multipart Question: Using detect and forward to resolve data hazards, and  predict not taken to resolve control hazards. Answer the statements below. [6 pts]
a.  How many cycles are required to empty out the pipeline (at the end of a program) [1.5]
b.  How many instructions are run in this program? [1.5]
c.  With parts a) and b) in mind, how many cycles does the program take to run? [3]
Question 2: Detecting Hazards in LC2K Code (Version 2) [12 points]
Suppose the following LC2K assembly code is run through the 5-stage pipeline from lecture until it halts.

1. Select all registers that cause a RAW (Read after write) data hazard in a detect and stall pipeline. Assume that data hazards are resolved with detect and stall. Assume that control hazards are resolved with detect and stall. Data hazards can only occur from instructions that are executed. [3 pts]a.  reg0 b.  reg1 c.  reg2 d.  reg3 e.  reg4 f.   reg5 g.  reg6 h.  reg7
2.  Using detect and stall to resolve data hazards, and detect and stall to
haza(reso)lrd(ve)sc?o[3(n)t pt(ro)lsh]azards, what is the number of stalls that occur only due to data3. Multipart Question: Using detect and forward to resolve data hazards, and  predict not taken to resolve control hazards. Answer the statements below. [6 pts]
d.  How many cycles are required to empty out the pipeline (at the end of a program) [1.5]
e.  How many instructions are run in this program? [1.5]
f.   With parts a) and b) in mind, how many cycles does the program take to run? [3]
Question 2: Detecting Hazards in LC2K Code (Version 3) [12 points]
Suppose the following LC2K assembly code is run through the 5-stage pipeline from lecture until it halts.

1. Select all registers that cause a RAW (Read after write) data hazard in a detect and stall pipeline. Assume that data hazards are resolved with detect and stall. Assume that control hazards are resolved with detect and stall. Data hazards can only occur from instructions that are executed. [3 pts]a.  reg0 b.  reg1 c.  reg2 d.  reg3 e.  reg4 f.   reg5 g.  reg6 h.  reg7
2.  Using detect and stall to resolve data hazards, and detect and stall to
haza(reso)lrd(ve)sc?o[3(n)t pt(ro)lsh]azards, what is the number of stalls that occur only due to data3. Multipart Question: Using detect and forward to resolve data hazards, and  predict not taken to resolve control hazards. Answer the statements below. [6 pts]
g.  How many cycles are required to empty out the pipeline (at the end of a program) [1.5]
h.  How many instructions are run in this program? [1.5]
i.   With parts a) and b) in mind, how many cycles does the program take to run? [3]
Question 3: P代 写EECS 370 Final Exam Winter 2021R
代做程序编程语言ipeline Datapath Design [15 points - Each blank 0.75 point]
In order to speed up pointer dereferences, Salar adds two instructions to LC2K with the following semantics:
Pointer Load Word
plw regA regB offset // regB = memory[ memory[regA + offset]  ]
Pointer Store Word
psw regA regB offset // memory[ memory[regA + offset]  ] = regB
Salar also breaks up the memory stage of the 5-stage pipeline into two stages:  MEM1 and MEM2.In MEM1, plw and psw load the pointer from memory. lw and sw access data memory in MEM1. In MEM2, plw loads the data from the pointer address in memory. psw stores the value of regB   to the pointer address in memory.Q3.1) Salar provisions one data memory read/write port that allows only one read or write in any cycle.  This introduces a structural hazard:  MEM1 and MEM2 cannot access data memory in   the same cycle.
We use detect and stall to address this hazard by stalling the IF and ID stages and inserting
Noop(s) into the id_ex register.  All the data forwarding is also done to EX stage. We want to     simulate our new pipeline, similar to project 3.  Below, complete the C expression so that the    bool is true if and only if our simulated pipeline should stall for the structural hazard.  Use the    pipeline registers, constants, variables, and helper functions from the Simulation Appendix at the end of the problem.
bool stall_for_structural_hazard =
( opcode( if_id.instr ) == PLW
|| opcode(  (1)  ) == (2)
|| opcode(  (3)  ) == (4)
|| opcode(  (5)  ) == (6) )

( opcode(  (7)  ) == (8)
|| opcode(  (9)  ) == (10) );(1) (2) (3) (4) (5)(6)   (7)   (8)   (9)   (10)
Q3.2) Our new instructions also introduce data hazard(s) that require a stall.  Below, complete the C expression so that the bool is true if and only if our simulated pipeline should stall for a   new data hazard.  As before, we stall the IF and ID stages and insert Noop(s) into the id_ex register.  This expression should NOT account for the pre-existing data hazard stall due to LW.
bool stall_for_new_data_hazard =
( opcode(id_ex.instr) == PLW
 regA(if_id.instr) != -1
 regA(if_id.instr) == regB(id_ex.instr) )
||
( opcode(id_ex.instr) == PLW
 regB(if_id.instr) != -1
 regB(if_id.instr) == regB(id_ex.instr) )
||
( opcode( (1) ) == (2)
 (3) != -1
 (4) == (5) )
||
( opcode( (6) ) == (7)
 (8) != -1
 (9) == (10) );(1)   (2)   (3)   (4)   (5)   (6)   (7)   (8)   (9)   (10)
Simulation Appendix:




Question 4: Pipeline Performance (Version 1) [14 points]
Consider a 1GHz version of an LC2K pipelined processor (as described in class, using detect-and-forward as well as predicting not-taken). You have been     looking into designing a new, 1.4GHz version of the processor.
●   However, this higher frequency has come at the cost of increasing the number of cycles for all operations in the ALU to complete by one. So, our new pipeline now has 6 stages (IF, ID, EX1, EX2, MEM, and WB).
●   The processor is still fully pipelined, and every other stage works exactly the
same. Branches are resolved in the MEM stage and data is always forwarded to EX1 stage.
●   Assume a benchmark with the following characteristics will be run on the original


15% instructions are loads
●   20% instructions are stores


●   30% instructions are adds
●   25% instructions are nors
●   10% instructions are branches
●   30% of instructions are dependent on the instruction immediately in front of them
●   10% of instructions are not dependent on the instruction immediately in front of them but are dependent on the instruction after that
●   For the above two lines you may assume that they are true no matter what instructions are involved.
●   The distribution of immediate and non immediate dependencies are exclusive from each other.
●   30% branches are taken.
In summary, we have two processors:


● Original: 1.0 GHz, 5 stages


●   New: 1.4GHz, 6 stages
Answer the following questions –
1.  Assuming no control or data hazards, what is the execution time of the two processors (Assume 100 instructions)? [2]
Processor
CPI
Execution Time
Original


New


2.  What is the CPI of the new processor (Taking data and control hazards into account, and now assuming infinite instructions)? [3]




3.  Explain the impact of adding the extra stage to the new processor on control hazards and data hazards (Consider the impact of the new cycle on control   hazards and data hazards separately) [3]
4.  Now consider an LC2K program with the following characteristics –

● 15% instructions are loads
● 20% instructions are stores


●   30% instructions are adds
●   25% instructions are nors
●   10% instructions are branches
●   30% of the instructions are dependent on the instruction immediately in     front of them. You may assume this is true no matter what instructions are involved.
●   30% of the branches are taken
●   (Note that percentage of each instruction and dependencies is the same as the new pipeline)
●   You may assume that infinite instructions are being executed
i)        What would be the expected CPI of your program using
detect-and-forward to resolve data dependencies and detect-and-stall for branches? Assume we are using the OLD pipeline (the one described in class). Clearly show your work. [3]
ii)        What would be the expected CPI of your program using
detect-and-forward to resolve data dependencies and predict-not-taken for branches? Assume we are using the OLD pipeline (the one described in class). Clearly show your work. [3]



         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
