# Building Block View

## Whitebox Overall System

**Inputs of building block view:**
 - use of a Raspberry Pico board with double core
 - use of gdb as debugger
 - Split firmware into services and tasks

Those are the main items of our project. For more details, see all decisions, requirements, context and goals made in previous step of ARC42 process, (steps 01 to 04)

With those directions, we may provide a first diagram about the highest level of architecture

![Hierarchy of building blocks](./images/Building_block_L1.png)
<div align="center"> architecture - building block level 1
<div align="left">

**Logical decomposition**

On the architecture overview, we split the system depending on their functional goals. The second decision was to split components which uses external code/library/framework (like the RTOS scheduler/core) from those we fully develop ourselves.

The annotation on each component (as well as the color) helps understand the decomposition.

**Contained building blocks:**

| Building block | Description |
|:-|:-|
|```RTOS_scheduler```| Real time os task and service scheduler |
|```service_list```| Container for all application software services  |
|```service_IO```| All *embedded* communication mean available during run-time |
|```service_encryption```| External library to do encryption |
|```service_database```| Manage non volatile and volatile big memory blocks |
|```service_sensors```| Everything which comes from the physical world |
|```interrupts```| Particular block, container which gathers interrupt handling |

**Important Interfaces**

| Interface | Description |
|:-|:-|
|```UI```| **U**ser **I**nterface,  interface between user system |
|```ssh```| **S**uper **SH**ell, used for debug, analysis and continuous integration |
|```ADC```| **A**nalog to **D**igital **C**onverter, interface to physical world |
|```flash memory```| Interface to file system |

## Building block description


### ```RTOS_scheduler```
**Purpose/Responsibility:**  
Real Time OS core and scheduler, here will be defined our RTOS behavior, which task/services call and so on. Every RTOS behavior relevant decision/development will be done here

**Interface(s)**  
All services in our program, except for interrupts block which is independent. They are all output.

**(Optional) Quality/Performance Characteristics**  
Quality goals are listed in [goals of RTOS](../00_Requirements_Inputs/01_introduction_and_goals_RTOS.md). There is a list of quality goals to reach, each one of them being good or bad. We will explore here the differences of quality between a well tailored RTOS from a quick and dirty RTOS massacre.

**(Optional) Directory/File Location>**  
code: [03_Development/code/src/RTOS_scheduler/](../03_Development/code/src/RTOS_scheduler/)

**(Optional) Fulfilled Requirements**  
 - [R1.3](../00_Requirements_Inputs/01_introduction_and_goals_RTOS.md), all RTOS requirement

**(optional) Open Issues/Problems/Risks**  
@todo


### ```service_list```
**Purpose/Responsibility:**  
Gather all application software we want to develop. It is a list, as application software need to be decomposed in services. Each app software topic in its own service.  
The idea here is for each of the developer to add a service if RTOS scheduling timings are still respected and have some fun in it, interfacing itself with other services. The developer must first develop its service architecture and agree with the others how he is going to add it in system.

**Interface(s)**  

| To service | direction | description |
|:-|:-:|:-|
| ```service_IO``` | in/out | use of ```service_IO``` to send and receive data to external world |
| ```RTOS_scheduler``` | in | Scheduler has the power to preempt/call/suspend tasks/services |

**(Optional) Quality/Performance Characteristics**  
Shall meet the allowed execution time and deadlines fixed for whole system in section
Task/service timings requirements

**(Optional) Directory/File Location>**  
code: [03_Development/code/src/service_list/](../03_Development/code/src/service_list/)

**(Optional) Fulfilled Requirements**  
 - [R1.7](../00_Requirements_Inputs/01_introduction_and_goals.md) Team work  
 - [R1.1](../00_Requirements_Inputs/01_introduction_and_goals.md) Programming language  
 - [Rx](../00_Requirements_Inputs/01_introduction_and_goals.md) Have fun  

**(optional) Open Issues/Problems/Risks**  
@todo


### ```service_IO```
**Purpose/Responsibility:**  
 All input/output which are not for continuous integration or debug will be in this one service. But each communication will have its own task. It is described as one service for logical reason: all same purpose stuff in one container.

**Interface(s)**  

| To service | direction | description |
|:-|:-:|:-|
| ```UI``` | in/out | implements the desired user interface |
| ```RTOS_scheduler``` | in | Scheduler has the power to preempt/call/suspend tasks/services |
| ```service_list``` | in | Is used by the different app software services to send/receive data  |

**(Optional) Quality/Performance Characteristics**  
Shall meet the allowed execution time and deadlines fixed for whole system in section
Task/service timings requirements

**(Optional) Directory/File Location>**  
code: [03_Development/code/src/service_IO/](../03_Development/code/src/service_IO/)

**(Optional) Fulfilled Requirements**  
 - [R1.3.6.1](../00_Requirements_Inputs/01_introduction_and_goals_RTOS.md): Service interrupt art
 - [R1.3.4.x](../00_Requirements_Inputs/01_introduction_and_goals_RTOS.md): User can activate bad or good code through IO

**(optional) Open Issues/Problems/Risks**  
@todo


### ```service_encryption```
**Purpose/Responsibility:**  
A heavy computing service which uses an external library. The library may be dynamically loaded while running or statically linked during compile phase. Its main purpose is to encrypt and decrypt data, while using a lot of CPU time and some shared resources.
The service encrypt and decode data from database in memory. This data is shared with another service in the ```service_list``` container.  

**Interface(s)**  

| To service | direction | description |
|:-|:-:|:-|
| ```RTOS_scheduler``` | in | Scheduler has the power to preempt/call/suspend tasks/services |
| ```service_database``` | out | Get data to be encrypted/decoded from critical shared resource  |
| ```service_list``` | in | (not decided) May be used by some application software to encrypt/decode data |

**(Optional) Quality/Performance Characteristics**  
Shall meet the allowed execution time and deadlines fixed for whole system in section
Task/service timings requirements

**(Optional) Directory/File Location>**  
code: [03_Development/code/src/service_encryption/](../03_Development/code/src/service_encryption/)

**(Optional) Fulfilled Requirements**  
 - [R1.3.6.2](../00_Requirements_Inputs/01_introduction_and_goals_RTOS.md): Heavy computing service, like AES encoding.
 - [R1.3.4.x](../00_Requirements_Inputs/01_introduction_and_goals_RTOS.md): Code efficiency

**(optional) Open Issues/Problems/Risks**  
 - Which encryption is still to be defined  
 - There is a risk that some encryption libraries are too big for memory and CPU capacities.


### ```service_database```
**Purpose/Responsibility:**  
Takes care of memory management. It is either volatile or non volatile, a file system or simple  C malloc() or whatever but it takes care to save data on memory for the system. It is a *critical* shared resource.

**Interface(s)**  

| To service | direction | description |
|:-|:-:|:-|
| ```RTOS_scheduler``` | in | Scheduler has the power to preempt/call/suspend tasks/services |
| ```service_encryption``` | in | Get its data to encrypt from memory |
| ```service_list``` | in | (not decided) Other user of the critical shared resource. May block ```service_encryption``` and create some priority inversion  |
| ```service_sensors``` | out | (not decided) Sensors may be write directly into memory |
| ```interrupts``` | out | (not decided) Interrupts may quick save some data into memory |


**(Optional) Quality/Performance Characteristics**  
Shall meet the allowed execution time and deadlines fixed for whole system in section
Task/service timings requirements

**(Optional) Directory/File Location>**  
code: [03_Development/code/src/RTOS_scheduler/](../03_Development/code/src/RTOS_scheduler/)

**(Optional) Fulfilled Requirements**  
 - [R1.3.1.2](../00_Requirements_Inputs/01_introduction_and_goals_RTOS.md): Mutexes and semaphores
 - [R1.3.4.4](../00_Requirements_Inputs/01_introduction_and_goals_RTOS.md): Memory leak
 - [R1.3.6.4](../00_Requirements_Inputs/01_introduction_and_goals_RTOS.md): slow service


**(optional) Open Issues/Problems/Risks**  
 - Risk of too few place available in memory
 - Risk of external memory use which complicates system


### ```service_sensors```
**Purpose/Responsibility:**  
Provide values and events coming from the physical world. It is a kind of interaction with the system. Like ```service_IO``` each sensor should have its own task. The described service here is more like a container

**Interface(s)**  

| To service | direction | description |
|:-|:-:|:-|
| ```RTOS_scheduler``` | in | Scheduler has the power to preempt/call/suspend tasks/services |
| ```service_database``` | out | (not decided) save data to memory |
| ```ADC``` | out | (external) Analog to digital converter interface  |

**(Optional) Quality/Performance Characteristics**  
Shall meet the allowed execution time and deadlines fixed for whole system in section
Task/service timings requirements

**(Optional) Directory/File Location>**  
code: [03_Development/code/src/service_sensors/](../03_Development/code/src/service_sensors/)

**(Optional) Fulfilled Requirements**  
 - [R2](../00_Requirements_Inputs/01_introduction_and_goals.md): work in an embedded environment
 - [R1.3.6.3](../00_Requirements_Inputs/01_introduction_and_goals_RTOS.md): Polling art

**(optional) Open Issues/Problems/Risks**  
@todo


### ```interrupts```
**Purpose/Responsibility:**  
Container which gathers all interrupt callbacks, it is RTOS independent and may preempt full system as its priority is most of the time maximal (except for task of fatal level)

**Interface(s)**  

| To service | direction | description |
|:-|:-:|:-|
| ```service_database``` | out | (not decided) save data to memory |

**(Optional) Quality/Performance Characteristics**  
All interrupts must be as fast as possible, as they are not scheduled by RTOS and are unpredictable. Which will overhead for the whole system and prevent deterministic behavior.  
Some maximum rating and worst-case scenario shall be described to limit interrupts allowed overhead time.

**(Optional) Directory/File Location>**  
code: [03_Development/code/src/interrupts/](../03_Development/code/src/interrupts/)

**(Optional) Fulfilled Requirements**  
 - [R1.3.6.1](../00_Requirements_Inputs/01_introduction_and_goals_RTOS.md): Memory leak
No other particular functional requirement directly fulfilled with this container. But it is mandatory for the rest of the system to work

**(optional) Open Issues/Problems/Risks**  
 - wrongly programmed, interrupt may simply kill our RTOS determinism design.
 - They are described in our code, but are strongly hardware architecture dependent


## Interfaces description

### ```UI```
**U**ser **I**nterface, is the logical interface between user (may be human or another system) and our system. It is an embedded communication mean like CAN, I2C or USART. It may be used by all of the application software services (component ```service_list```)

### ```ssh```
**S**uper **SH**ell, used for debug, analysis and continuous integration. It touches the whole system and will allow us to do some deep performances analysis.

### ```ADC```
**A**nalog to **D**igital **C**onverter, is our interface to physical world. It may be stubbed or not really exists, its main purpose is to watch something moving and have fun.

### ```flash memory```
Is the interface to our file system. Depending on our hardware target, it may be the interface to a flash storage or a full file system on a hard drive like an SSD.



See [Building Block View](https://docs.arc42.org/section-5/) in the
arc42 documentation.
