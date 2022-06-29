# Architecture Constraints

The aim of this project is to work with some friends which may easily join the project and train themselves. The team work is also a goal of this project for us to train to work with other actors and stakeholders in a project.  
For this reason, the needed hardware/infrastructure should be as cheaper as possible.

## Organization constraints

| ID  | Description |
|-------------|:-------------------------|
| *O1* | *Project is a sandbox and contributors will likely want to concentrate development on their own interest. The project must keep a common goal*   |
| *O2* | *Resources needed for project should be as light as possible (costs, place, availability...)* |
| *O3* | *The project shall be IDE independent, as many people love to use their own environment. And also because it is possible to have a full project without the need of an IDE* |
| *O4* | *For organizational easiness, only one hardware target will be used at the beginning* |

## Technical constraints

| ID  | Description |
|-------------|:-------------------------|
| *T1* | *The chosen RTOS should be free to download and use. No money cost should be needed.*   |
| *T2* | *The chosen hardware should not be expensive and easily available for newcomers to join the project* |
| *T3* | *The chosen hardware will need a CPU with at least two core for symmetric RTOS* |
| *T4* | *Unit test will be applied on one hardware target only* |
| *T5* | *The project will be oriented to embedded systems, which means the use of a micro-controller and some hardware* |
| *T6* | *The project is versioned on github with git* |
| *T7* | *Code management system (git) should not be used to save executable files or any compiled program of any kind. Its purpose is to save the code, any executable files or program needed for code must be exchanged another way*   |

## Conventional constraints
| ID  | Description |
|-------------|:-------------------------|
| *C1* | *TODO - Coding conventions must be respected (naming conventions, indentation, UTF-8 characters only, ANSI-C standard, ...)*   |
| *C2* | *Coding: all source code must respect UTF-8 encoding, any other character should not be used*   |
| *C3* | *C and C++ programming will use their last respective defined standards*   |



See [Architecture Constraints](https://docs.arc42.org/section-2/) in the
arc42 documentation.
