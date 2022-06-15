# RTOS Introduction and Goals

This document gathers RTOS specific requirements and quality goals.

## RTOS functional requirements Overview

This sub sections of introduction and goals explains what we want to learn/observe on an RTOS service. There are some RTOS principle we want to discover, understand how rightfully/wrongly coded program may work or not, try different RTOS behavior and so on.

### RTOS Principles:
 - **R1.3.1.1** priority inversion problem
 - **R1.3.1.2** Mutexes and semaphores (shared ressources)
 - **R1.3.1.3** Reentrant functions (Thread safe)

### RTOS behaviors:
 - **R1.3.2.1** Hard RTOS
 - **R1.3.2.2** Soft RTOS
 - **R1.3.2.3** Different schedulers policies: fixed priority, dynamic priority
 - **R1.3.2.4** Different priority policies: Rate monotonic,Deadline monotonic

### RTOS architecture:
 - **R1.3.3.1** Design a fully deterministic architecture, where maximal capacity of device may be calculated and presented as a quality goal. Best use of CPU should be done anyway
 - **R1.3.3.2** Design a 100% CPU usage architecture where determinism is not priority. Best deterministic architecture should be anyway used

### Code optimization for better efficiency
 - **R1.3.4.1** Proper use of L1 cache/processor architecture
 - **R1.3.4.2** Functions inlining
 - **R1.3.4.3** Compiler optimizations
 - **R1.3.4.4** Memory management and memory leak detection (Valgrind)

### Debug and test
 - **R1.3.5.1** Make an analysis of task time slot allocation (have 100% CPU time used), check mathematically
 - **R1.3.5.2** Unit test of tasks, check if they fit in their allowed time
 - **R1.3.5.3** Profiling of RTOS with use of gdb and/or a task time viewer

### Non RTOS features:
Those features will "fill" the different task's purpose. They are typical services we may meet in RTOS all day life. They may be of interrupt art, heavy computing time, polling art or shared ressource/slow time art.

 - **R1.3.6.1** Service interrupt art: communication SPI, I2C, UART, CAN (not on all uC)
 - **R1.3.6.2** Service heavy computing time art: encryption (AES), FFT or signal processing, artificial intelligence/machine learning
 - **R1.3.6.3** Service polling art: sensors input
 - **R1.3.6.4** Service slow time art: wait for a sub task or peripheral to finish job

## Quality Goals

## The good code, the bad code and the ugly code:
As in this marvelous western, aim of this project is also to see that some small stuff may kill the full system's behavior and make our product unstable and useless.  
All the different features listed before will have a good code as well as a bad (doesn't fulfill requirement) and an ugly code (don't work in some case)  

There are 3 elements to be careful for a stable and optimized RTOS service:
 - **Q1.3.1** Taking care of uC/uP architecture and how we code (cache, stack, Mutexes, reentrant functions...)
 - **Q1.3.2** Choose the right RTOS behavior (scheduler and priority policy)
 - **Q1.3.3** Choose the right task time slot allocation

Different code will be developed to show that if one of those is wrongly made, the system can't match the expected requirements. To do that, those different code will compiled in different static libraries and chosen during linking with CMake. Or compiled in dynamic library and program will switch from good to bad to ugly library while running, as human ask for it through an I/O command (like an SPI message which orders program to use bad functions lib instead of good).

 -  **R1.3.7.1** The good code:  
The good code will show that with optimized code for architecture, with the good RTOS behavior (Scheduler and priority policies) and a good analysis (task profiling), the required service works always and is table in the time  

 - **R1.3.7.2** The bad code:  
The bad code will show that the system, if one of the three elements (coding, RTOS behavior and task time allocation) is wrongly made, the required service simply don't work.

 - **R1.3.7.3** The ugly code:  
The ugly code will be as this filthy guy in the movie, it will work, but not always. Some situations like after a long time, or a bad profiled task time allocation may lead in some situation to a bottleneck, deadlock or a deadline missed.
