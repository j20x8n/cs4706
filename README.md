java c
Mini-MIPS   CPU
COMP   273   Project
Due:   December 8, 2024, on   MyCourses
Submission   instructions
You can do this   project on your own   or   in   a team   of   2   students.   All   work   must   be   your   own   and   must   be submitted to   myCourses.   Include your   name(s) and student   number(s) in a comment   at the   top   of your   Logisim circuit. Submit only one file:   project-miniCPU.circ   per group. Check your   submission   by   downloading   it from   myCourses to verify that   it was correctly submitted.   You will   not   receive   marks   for   work that is incorrectly   submitted.
You   must enroll yourself   in a group on   MyCourses   to   be   able to   submit the   project.   If you   are   working   on   your own, you must still enroll yourself in   a group   on   MyCourses.
Purpose
•            Understand   how CPUs function.
•          To   understand how the CU coordinates the different   machines that   make the   CPU.
Helpful
•          The   lectures on   Datapath   and   CU.
•          Optionally you may   use your A2   solutions   for ALU   and   RAM   (the   graded   version)   in   this   project.
   
Figure 1 - Mini-MIPS architecture
Overview
Mini-MIPS   is a CPU that executes only   one   instruction   at   a time.   This   means   it   executes   the   instructions   sequentially, one   by one.
The   Mini-MIPS CPU diagram,   Figure   1,   is the   basic CPU architecture that   everyone’s   project   must   adhere   to.   It   represents the   basic architecture. The TA will   make sure that your   CPU   looks   and   behaves   as   like the above diagram. You are   permitted to   build the   entire   CPU on   the   same   circuit   page,   or   you   can create subcircuit   pages to   mimic the above diagram’s   look.   If you   build your   CPU   on   a   single   page,   it   is important to   label each   part of the circuit and   to   leave   empty   spaces   to   separate   the   parts.   This will   both help you while debugging and help the TA   understand what you   have   built.   If you   chose   to   use subcircuits you will   need to take care of the time delays   that   Logisim   adds to   subcircuits.   The   more   subcircuits you   nest the   more delays are   added.
The execution of a single   instruction   requires   multiple tricks. The   CU,   not shown,   controls   each   section   of the   instruction execution cycle. The execution   cycle   constitutes of   the   fowllowing   stages:Stage 0:   Loads an   instruction from the   instruction   RAM   using the address stored   in   PC   into   IR      (notice      RAM and   not cache – we are   using your   A2   RAM   to   make   things   easier).   PC   is   incremented   to   the   next   address   (circuit   not shown   in diagram). This completes Stage 0.
Stage   1:   Uses the   Register file to output the values for the ALU’s   input   registers   (not   shown   in   the   diagram).   Bits from the   IR will address the specific   Register file   registers.
Stage 2: The ALU   performs the selected operation   updating the   status   register   and ALU   output   register            (not shown   in the diagram) and sending values to   intermediate   registers   (not   shown   in   diagram)   for   the         multiple data   paths that are   possible at this   point   in execution   (to   prepare   for:   an   overwrite   of the   PC,   or   overwrite   Data   RAM at a specific address,   or overwrite   a   specific   register   in   the   Register   file).
Stage 3: Completes what was   prepped   by Stage 2:   either   write   into   Data   RAM   at   a   particular   address   or   loads a value from   Data   RAM   into the input of the Register file   or   overwrites   the   PC,   etc.
Stage 4:    Completes the write to   Register file from   stage   3   (if   needed)   and then the   CU   loops   back   to   Stage 0. The CU operates as   an   infinite   loop   until   the   program   asks the   computer   to   shutdown.

Your final submission   must   run   by auto ticking at the   default   Logisim   Evolution   1   Hz   rate.   When   you   test      your circuit, you can   manually click on the clock,   but   the   final   submission   must   auto   tick.   You   can   set   this   up through the   menu option Simulate, see   Figure 2.   Make sure “Auto-propagate”   is   check   marked.   Make   sure “Auto Tick”   is check   marked.   Make sure “Auto tick frequency”   is set   to   1   Hz.      If   you   circuit   runs   at   1      Hz   it will   run at   higher frequencies as well.   But the TA   will   test   your   circuit   with   the   default   speed.From the Simulate tab you can start and stop the ticking,   see   Figure   3. The   play   and   pause   buttons can   be   pressed to start and stop the ticking of the   clock.   When   you   pause   the   clock,   you   can   manually   tick   the clock. When you   press   play,   it will   resume ticking where   you   left of.   Figure   2
   Figure   3


Implementation
Using Logisim   Evolution create the following Mini-MIPS CPU:
•          To   make things easier: everything   is   a   nibble   in size.   All   data   area   nibble   (4-bits). The   IR   must   be   able to address a   maximum   of 8   代 写COMP 273 Project Mini-MIPS CPUR
代做程序编程语言nibbles.
•          Your circuit must   have the following   components:
o   A   clock
o   The CPU-parts depicted   in figure   1 and   described   in Overview.
o   The   Register file only   has two   registers:   R0 and   R1.
o   The CU controls everything   inside the   CPU.
o   The Status   register flags: Sign overflow,   zero, and   negative.
o   Instruction   RAM stores 8   nibbles of   data.
o   Data   RAM stores   2   nibbles of   data.
o   The CU   must   implement the   Fetch and   Execute   instruction.
o   You can add additional components to   help you.   See the   list   of   legal   components.
•          You are   permitted to ONLY   the following Logisim   pre-built   elements:
o   Clock
o   Wire and splitters.
o   D-Flip-flop and Register.
o   AND, OR,   NOT, XOR,   Buffer, and controlled   buffer gates
o   Pins and   probes
o   Subcircuits (optional)
o   Tunnelling (optional)
o   Multiplexer
o   Decoder
NOTE   1   : The TA   must   be able to   change   and see the   bits   of   RAM and   registers   before   and   after   execution.   Provide   away for this   to   happen   (this   is   especially   important for those   of you   using   subcircuits).
NOTE 2: Your final circuit must   use   designs we   covered   during   class. You   cannot   use   any   outside   (other   sourced) circuit designs.
Instructions
•          The   Instruction   RAM   has 8 nibbles. These   nibbles will   be   used to   store   the   machine   codes of your assembler instructions. Algorithms   must fit within this   space   and terminate with   HALT.
•          The   Data   RAM   has 2   nibbles   and will store the   program’sdata.
•          To   run a   program, you will   need to first   input   the   instructions   into   the   Instruction   RAM,   the   data   in the   Data   RAM, and set the   PC   pointing to the first   instruction   in the   Instruction   RAM. All other   registers are assumed to   be zero or   overwritable. Then   the   auto-clock   is   turned   on   and   the programs   runs.   Make sure to   place the   clock on your   circuit.
•            LOAD   REGISTER,   RAM_ADDRESS
o   1st    2   bits   :   LOAD   = 00
o   3rd    bit   :   REGISTER =   0 for   R0,   1   for   R1
o   4th    bit   :   RAM_ADDRESS = 0 for address 0   in   RAM,   1 for address   1   in   RAM
o   Example:   LOAD   R1, 0      0010
o   Example:   LOAD   R0,   1      0001
•          SAVE   REGISTER,   RAM_ADDRESS
o   1st    2   bits   : SAVE   =   01
o   3rd    bit   :   REGISTER =   as   in   LOAD
o   4th    bit   :   RAM_ADDRESS   =   as in   LOAD
o   Example: SAVE   R0,   1      0101
•          ADD   REGISTER1   REGISER2
o   1st    2   bits   : ADD   =   10
o   3rd    bit   :   REGISTER =   as   in   LOAD
o   4th    bit   :   REGISTER =   as   in   LOAD
o   The solution to the addition   is saved in   REGISTER1.
o   Example: ADD   R1   R0      R1 =   R1 +   R0      1010
o   Example: ADD   R0   R0      R0 =   R0 +   R0      1000
•            SUB   REGISTER1   REGISTER2
o   1st    2   bits   :   SUB   =   11
o   3rd    bit   :   REGISTER =   as   in   LOAD
o   4th    bit   :   REGISTER =   as   in   LOAD
o   The solution to the subtraction   is saved   in   REGISTER1.
o   Example: SUB   R1   R0      R1 =   R1 –   R0      1110
o   Example: SUB   R0   R0      R0 =   R0 –   R0      1100
•            HALT
o   All four   bits   are   1.
o   Example:   HALT      1111
o   This   marks the end of the algorithm. The clock’sticking does   not affect the circuit   anymore. The   PC   no   longer   increments.
•            Bonus   instruction:
o   JUMP
               Use   machine code 0000 for   jump “j” instruction.   PC   is   updated with whatever   is in   R0.
•          Your circuit   must   be able to   execute   any   program   set   in the   RAM with the   PC   pointing   to the   first   instruction of that algorithm. The   PC can   be set to   any   starting   address.
Execution
Your CPU circuit   must   be able to do at   least the following   algorithms:
1.          Execute a   program that loads two   numbers,   performs an   ALU   operation,   and then   saves the   solution.
2.          Execute aprogram that   has only the   HALT   instruction.
Note: The TA will test your CPU   by first entering   a   starting   address   in the   PC   and   loading   a   program         in your   Instruction   RAM and data   in your   Data   RAM. Then, they will start the clock   and   see   the   result   display   in the   Data   RAM.
Note: Your CPU does   not   need to   be optimized, therefore   it does   not   matter the   number of   clock   ticks   it   needs to execute your   instructions.
Marking
•            Bonus   points for JUMP +3
•            Maximum   100   points
o   +10   Reusing A2 circuits.
o   +20   Using one common clock for   the circuit
o   +20   Complete   Datapath   implementation   (including   buses   between the different   components)
o   +10 CPU   Registers   R0 and   R1.
o   +10   PC   Increment.
o   +30 CU and execution   of   instructions.
•            -20   points for   not   using the clock.

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
