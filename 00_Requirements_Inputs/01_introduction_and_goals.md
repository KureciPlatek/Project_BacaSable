# Introduction and Goals {#section-introduction-and-goals}

The aim of this project is to focus on the understanding and train of some technologies inside one small-scale project, without any particular application software on it.
The technologies are divided into three sub categories:
 - technological principles
 - technological tools
 - technologies itself

Some of the targeted items in this project, needs an application software to be done (example: for artificial intelligence). It is then free to develop any application we want, as long as it fits inside the project (small scale).  
The number of used technologies may vary and will surely evolve in the future, depending on needs.

## Requirements Overview

### R1 - Technologies
The mandatory technologies used are following:
 - **R1.1** Programming language:  
The programming language used shall be C/C++ in embedded world. Some assembler code may also be used.

 - **R1.2** Low level programming:  
After choice of hardware target, the architecture of CPU shall be explored and understood to optimize the code against it (good use of registers, assembler programming, function inlining, proper use of L1 cache...).

 - **R1.3** Memory management:  
As every program needs memory to work, how to properly use memory, especially with C/C++ and its stack/heap shall be explored. A memory leak/profiler tool shall also be used (described in section R2 - Tools).

 - **R1.4** Encryption:  
Cyber security and safety is becoming a predominant part of our work as a compute science engineer. Therefore, encryption principle and attack test shall be done on product.

 - **R1.5** Hardware architecture optimization:  
Some code parts shall show optimized performances, depending on the used hardware architecture (available registers, MAC, ALU, FPU...), for that, some fancy assembler code may be developed



## R2 - Tools  
List of tools which shall be explored:

 - **R2.1** Debugger:  
A debugger shall be used to be able to track code efficiency, be able to capture and decode exception handling in a uC, or understand uC specific debugging environment (ex CoreSight of ARM architectures). All of that in a C/C++ programmed code on an RTOS environment.  

 - **R2.2** Compiler:  
Different optimization possibilities and pragma/compiler options in code shall be also discovered to understand the impact on program efficiency.

 - **R2.3** Project management:  
CMake shall be used to manage project source code, compiling and unit testing as well as some task automation, like scripting.

 - **R2.4** Memory leak/fragmentation/management:  
Memory management tools shall also be used to understand how to profile the memory, check for potential memory leak, avoid overflows and so on (like check heap and stack sanity).

 - **R2.5** RTOS profiling:  
As our environment of execution will be a real time OS, a task profiler tool shall be used to prove determinism execution of our code and CPU use efficiency.

## R3 - Principles
List of technological principles to be explored in this project. The list has high chance to evolve, because new application principles may be explored in the future.

 - **R3.1** Real Time Operating System:  
As RTOS are more and more used, as well as more and more efficient, the program shall be run on an RTOS environment. It means, that the project shall understand technological principles of an RTOS. For more details about RTOS goals, please look at [this file](01_introduction_and_goals_RTOS.md)  

 - **R3.2** Development process:  
There are TOO MANY development process and are sometimes too heavy for a small scale project. Nevertheless, some are getting more and more optimized and democratized in industries. An easy, modern and well spread development process shall be used (continuous integration, unit test...).  

 - **R3.3** Team work:  
Alone, we are faster, but together we are stronger. Principles of working in a team (if possible, people should join the project) shall be applied (scrum, agile...). This requirement is linked with R3.2, Dev Process.  

 - **R3.4** Architecture and documentation:  
The principles of architecture design and documentation provided by ARC42 shall be used (this document is part of it).  

 - **R3.5** Artificial Intelligence:  
Basic principles of artificial intelligence may be explored here, using the required technologies (RTOS, C/C++). As the project is small scale, create a powerful AI may only be done in another step. Nevertheless, discover main principles may be done here.

 - **R3.** Have fun.

## Quality Goals
the following quality goals are also principles or tools to be understood and/or improved.

### Q1 Code quality
#### Q1.1 Static code analysis:  
A static code analysis shall applied to code with a tool. Level of quality to be reached is still to be defined

#### Q1.1 Dynamic code analysis:  
A dynamic code analysis shall also be applied to code. It is a complex quality quality goal as the program is running under a multi-tasking real time OS. Level of quality is still to be defined

### Q2 memory management
A memory analysis tool/profiler shall be used to check for memory leak due to memory segmentation or any kind.  
The program shall run for 10 minutes and not present any kind of segmentation leading to memory leak and still have the same quantity of free memory, with a difference of 1% allowed.

### Q3 RTOS efficiency

RTOS quality requirements are defined in [this file](01_introduction_and_goals_RTOS.md).  

## Stakeholders


| Role/Name   | Contact                   | Expectations              |
|-------------|:-------------------------:|:-------------------------:|
| *Jeremie Gallee* | *galleej@gmail.com*  | *Have fun*        |
| *Florent Chretien* | *flopubs@gmail.com* | *Have fun*        |
