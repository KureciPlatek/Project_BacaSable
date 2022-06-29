# RTOS Introduction and Goals

This document gathers RTOS specific requirements and quality goals.

****  
## RTOS functional requirements Overview

This sub sections of introduction and goals explains what we want to learn/observe on an RTOS service. There are some RTOS principle we want to discover, understand how rightfully/wrongly coded program may work or not, try different RTOS behavior and so on.

The following requirements are all subdivisions of requirement **R3.1** from [01_introduction_and_goals](01_introduction_and_goals.md) file. They are all principles to be discovered.

_RTOS coding_:
 - **R3.1.1** The program shall be able to show a case with priority inversion problem
 - **R3.1.2** The program shall use mutexes and semaphores on a shared critical resource
 - **R3.1.3** The program shall use cases of thread safe functions (re-entrant)

_RTOS behaviors_:
 - **R3.1.4** The program shall be able to be activated either as hard or soft RTOS
 - **R3.1.5** The program shall use different schedulers policies: fixed priority, dynamic priority
 - **R3.1.6** The program shall present cases of different priority policies: rate monotonic, deadline monotonic and other if exists
 - **R3.1.7** The program shall have either symmetric multi-core or asymmetric multi-core behaviors
 - **R3.1.8** The program shall have present all combinations of RTOS possible behaviors (functional requirements R3.1.4 to R3.1.7) which makes 16 different combinations.

_RTOS analysis_:
 - **R3.1.5.3** The RTOS program tasks shall be profiled with use of a gdb and/or a task time viewer
 - **R3.1.5.1** Make an analysis of task time slot allocation (have 100% CPU time used), check mathematically

****  
## Quality Goals

Two different scenarios of RTOS will be tested in their qualities: a HARD RTOS and a SOFT RTOS.  
A hard RTOS always fulfill its deadlines (deterministic)  
A soft RTOS maximise CPU use and allows some deadlines to be missed (best effort)

 - **Q3.1** The HARD RTOS shall present a CPU use of at least 80% and in any case be deterministic.
    - **Q3.1.1** All HARD RTOS tasks must be unit tested for their running time and 100% shall meet their allocated time
    - **Q3.1.2** All HARD RTOS task shall be profiled and their time allocation calculated to meet a 80% use of CPU  


 - **Q3.2** the SOFT RTOS shall present a CPU use of 100% without need of perfect deadline respect.
    - **Q3.2.1** Soft RTOS shall never freeze and even if inputs rate is too high for soft RTOS's program, code shall be able to release tasks or drop some duties.
