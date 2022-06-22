# Introduction and Goals {#section-introduction-and-goals}

The aim of this project is to develop, train and maintain some technologies inside one project with maybe some sub-projects.
The number of used technologies may vary and i will surely evolve in the future, depending on needs.

## Requirements Overview

### R1 - Technologies
The mandatory technologies used are following:
 - **R1.1** Programming language:  
The programming language used shall be <strong>C/C++</strong> in embedded world. Some assembler code may also be used.

 - **R1.2** Compiler / project management:  
<strong>CMake</strong> shall be used to manage project source code, compiling and unit testing as well as some task automation, like scripting.

 - **R1.3** Real Time OS:  
The project shall use an <strong>RTOS</strong> on symmetric or asymmetric cores. The RTOS shall propose hard and soft real time OS. For more details about RTOS goals, please look at [this file](01_introduction_and_goals_RTOS.md)

 - **R1.4** Debugging:  
<strong>gdb</strong> shall be used for debugging of multi threaded application.

 - **R1.5** Hardware architecture optimization:  
Some code parts shall show <strong>optimized</strong> performances, depending on the used hardware architecture, for that, some fancy assembler code may be developed

 - **R1.6** Testing:  
Unit test and hardware in the loop with may be done following the principles of <strong>devOps</strong>. It will improve the automation and development processes.

 - **R1.7** Architecture and team work:  
To train team work on a remote project, <strong>UML architecture</strong> shall be used as well as ARC42 documentation format.

### R2 - Environment
 - **R2.1** Embedded systems:  
 The project shall be oriented to __embedded systems__, which means the use of a micro-controller and some Hardware

### R3 - IDE
 - **R3.1** IDE independence:  
The project shall be __IDE independent__, as many people love to use their own environment. And also because it is possible to have a full project without the need of an IDE

### R4 - Hardware/target
 - **R4.1** Availability:  
The hardware shall not be expensive and easily available on Internet for newcomers to easily join the project

 - **R4.2** Offered features:  
The hardware shall have a CPU with at least two core for synchronous RTOS. Monocore RTOS shall also be possible to be executed on the hardware target.

### Rx Have fun
You know what to do

## Quality Goals

There are no quality goals, as the project is a sandbox
@todo, change it for different code and RTOS scheduling quality (good, bad and ugly)  

### Q1 Code quality
#### Q1.1 Static code analysis:  
The code shall fulfill a static code analysis level - @todo level is to be defined  

#### Q1.1 Dynamic code analysis:  
A dynamic code analysis shall also be used. It is a complex quality quality goal as the program is running under a multi-tasking real time OS. 

### Q2 memory management
The program shall not present memory leak due to memory segmentation or any kind. A full analysis of memory use shall be done (outch!)

## Stakeholders


| Role/Name   | Contact                   | Expectations              |
|-------------|:-------------------------:|:-------------------------:|
| *Jeremie Gallee* | *galleej@gmail.com*  | *Have fun*        |
| *Florent Chretien* | *flopubs@gmail.com* | *Have fun*        |
