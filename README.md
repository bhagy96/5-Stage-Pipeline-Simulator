# 5-Stage Pipeline Simulator

## Overview 

Designed and implemented a Pipeline Simulator, a simple timing simulator for a 5-stage pipeline processor where we are simulating simulating the stages themselves and
determining when to put stalls / pipeline bubbles).

Essentially we detect RAW hazards and support forwarding from
1. EXEC/MEM pipeline register to EXEC stage
2. MEM/WB pipeline register to EXEC stage


## Usage

The command-line parameters are:
- i : input trace file
- f : for enabling forwarding

Example of simulator run:

```
$ ./pipesim -i traces/instruction1.txt
Loading application...traces/instruction1.txt
Read file completed!!
Printing Application:
ADD r1 r2 r3
SUB r2 r3 r4
MULT r3 r1 r5
DIV r4 r3 r6
LW r5 r4
SW r5 r7
BNE r7 r8
Initializing pipeline...
Cycle IF ID EXEC MEM WB
0 * * * * *
1 ADD r1 r2 r3 * * * *
2 SUB r2 r3 r4 ADD r1 r2 r3 * * *
3 MULT r3 r1 r5 SUB r2 r3 r4 ADD r1 r2 r3 * *
4 DIV r4 r3 r6 MULT r3 r1 r5 SUB r2 r3 r4 ADD r1 r2 r3 *
5 DIV r4 r3 r6 MULT r3 r1 r5 * SUB r2 r3 r4 ADD r1 r2 r3
6 LW r5 r4 DIV r4 r3 r6 MULT r3 r1 r5 * SUB r2 r3 r4
7 LW r5 r4 DIV r4 r3 r6 * MULT r3 r1 r5 *
8 LW r5 r4 DIV r4 r3 r6 * * MULT r3 r1 r5
9 SW r5 r7 LW r5 r4 DIV r4 r3 r6 * *
10 SW r5 r7 LW r5 r4 * DIV r4 r3 r6 *
11 SW r5 r7 LW r5 r4 * * DIV r4 r3 r6
12 BNE r7 r8 SW r5 r7 LW r5 r4 * *
13 BNE r7 r8 SW r5 r7 * LW r5 r4 *
14 BNE r7 r8 SW r5 r7 * * LW r5 r4
15 * BNE r7 r8 SW r5 r7 * *
16 * * BNE r7 r8 SW r5 r7 *
17 * * * BNE r7 r8 SW r5 r7
18 * * * * BNE r7 r8
19 *

```

Note : Each line in the trace file contains the program counter (pc) of the branch instruction (in the form of a 24-
bit hexadecimal address), and whether that branch was actually taken (T) or not taken (N).

### Credits:

- The structural code was given by Prof. Nael Abu-Ghazaleh and Jason Zellmer. I have added the implementation and extension part of the simulator.
