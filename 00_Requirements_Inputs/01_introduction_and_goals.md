# Introduction and Goals {#section-introduction-and-goals}

The aim of this project is to develop, train and maintain some technologies inside one project with maybe some sub-projects.
The number of used technologies may vary and i will surely evolve in the future, depending on needs.

## Requirements Overview {#_requirements_overview}

### R1 - Technologies
The mandatory technologies used are following:
#### R1.1 Programming language:
The programming language used shall be <strong>C/C++</strong> in embedded world. Some assembler code may also be used.
#### R1.2 Compiler / project management:
<strong>CMake</strong> shall be used to manage project source code, compiling and unit testing as well as some task automation, like scripting.
#### R1.3 Real Time OS:
The project shall use an <strong>RTOS</strong> on symmetric and asymmetric cores. The RTOS shall propose hard and soft real time OS
#### R1.4 Debugging:
<strong>gdb</strong> shall be used for debugging of multi threaded application.
#### R1.5 Hardware architecture optimization:
Some code parts shall show <strong>optimized</strong> performances, depending on the used hardware architecture, for that, some fancy assembler code may be developed
#### R1.6 Testing:
Unit test and hardware in the loop with shall be done with <strong>Jenkins</strong> and be automatized with the development process
#### R1.7 Architecture and team work:
To train team work on a remote project, <strong>UML architecture</strong> shall be used as well as ARC42 documentation format.

### R2 - Environment
The project shall be oriented to embedded systems, which means the use of a micro-controller and some Hardware

### R3 IDE
The project shall be IDE independent, as many people love to use their own environment. And also because it is possible to have a full project without the need of an IDE

### R4 RTOS
To develop real time operating system skills at its full possibility, the chosen RTOS shall be able to be either Hard RTOS or Soft RTOS, and different scheduler may be used.

### R5 - Hardware/target
#### R5.1 Availability
The hardware shall not be expensive and easily available on Internet for newcomers to easily join the project
#### R5.2 Offered features
The hardware shall have a CPU with at least two core for synchronous RTOS. Monocore RTOS shall also be possible to be executed on the hardware target.

### R6 Have fun
You know what to do

## Quality Goals {#_quality_goals}

There are no quality goals, as the project is a sandbox

## Stakeholders {#_stakeholders}


| Role/Name   | Contact                   | Expectations              |
|-------------|:-------------------------:|:-------------------------:|
| *Jeremie Gallee* | *galleej@gmail.com*  | *Have fun*        |
| *Florent Chretien* | *flopubs@gmail.com* | *Have fun*        |