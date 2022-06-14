# Building Block View {#section-building-block-view}

::: formalpara-title
**Content**
:::

The building block view shows the static decomposition of the system
into building blocks (modules, components, subsystems, classes,
interfaces, packages, libraries, frameworks, layers, partitions, tiers,
functions, macros, operations, datas structures, ...) as well as their
dependencies (relationships, associations, ...)

This view is mandatory for every architecture documentation. In analogy
to a house this is the *floor plan*.

::: formalpara-title
**Motivation**
:::

Maintain an overview of your source code by making its structure
understandable through abstraction.

This allows you to communicate with your stakeholder on an abstract
level without disclosing implementation details.

::: formalpara-title
**Form**
:::

The building block view is a hierarchical collection of black boxes and
white boxes (see figure below) and their descriptions.

![Hierarchy of building blocks](images/05_building_blocks-EN.png)

**Level 1** is the white box description of the overall system together
with black box descriptions of all contained building blocks.

**Level 2** zooms into some building blocks of level 1. Thus it contains
the white box description of selected building blocks of level 1,
together with black box descriptions of their internal building blocks.

**Level 3** zooms into selected building blocks of level 2, and so on.

See [Building Block View](https://docs.arc42.org/section-5/) in the
arc42 documentation.

## Whitebox Overall System {#_whitebox_overall_system}

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
|```UI```| **U**ser **I**nterface, is the logical interface between user (may be human or another system) and our system. It is an embedded communication mean |
|```ssh```| **S**uper **SH**ell, used for debug, analysis and continuous integration. Touches the whole system |
|```ADC```| **A**nalog to **D**igital **C**onverter, is our interface to physical world. It may be stubbed or not really exists, its main purpose is to watch something moving and have fun |
|```flash memory```| Is the interface to our file system. It may be a full operational file system or a flash memory |

## Building block description

### ```RTOS_scheduler```
**Purpose/Responsibility:**  
Real Time OS core and scheduler, here will be defined our RTOS behavior, which task/services call and so on. Every RTOS behavior relevant decision/development will be done here

**Interface(s)**  
All services in our program, except for interrupts block which is independent

**(Optional) Quality/Performance Characteristics**  
Quality goals are listed in [goals of RTOS](../00_Requirements_Inputs/01_introduction_and_goals_RTOS.md). There is a list of quality goals to reach, each one of them being good or bad. We will explore here the differences of quality between a well tailored RTOS from a quick and dirty RTOS massacre.

**(Optional) Directory/File Location>**  
-

**(Optional) Fulfilled Requirements**  
From file [goals](../00_Requirements_Inputs/01_introduction_and_goals_RTOS.md), fulfill requirement R1.3

**(optional) Open Issues/Problems/Risks**  
-

### ```service_list```
**Purpose/Responsibility:**  
Gather all application software we want to develop. It is a list, as application software need to be decomposed in services. Each app software topic in its own service

**Interface(s)**  

**(Optional) Quality/Performance Characteristics**  

**(Optional) Directory/File Location>**  
-

**(Optional) Fulfilled Requirements**  
-

**(optional) Open Issues/Problems/Risks**  
-

### ```<service_IO>```
**Purpose/Responsibility:**  
 All input/output which are not for continuous integration or debug will be in this one service. But each communication will have its own task. It is described as one service for logical reason: all same purpose stuff in one container.

**Interface(s)**  
-

**(Optional) Quality/Performance Characteristics**  
-

**(Optional) Directory/File Location>**  
-

**(Optional) Fulfilled Requirements**  
-

**(optional) Open Issues/Problems/Risks**  
-

### ```service_encryption```
**Purpose/Responsibility:**  
A heavy computing service which uses a still to be defined external library. The library may be dynamically loaded while running or statically linked during compile phase. Its main purpose is to encrypt and decrypt data, while using a lot of CPU time and some shared resources.

**Interface(s)**  
-

**(Optional) Quality/Performance Characteristics**  
-

**(Optional) Directory/File Location>**  
-

**(Optional) Fulfilled Requirements**  
-

**(optional) Open Issues/Problems/Risks**  
-

### ```service_database```
**Purpose/Responsibility:**  
Takes care of memory management. It is either volatile or non volatile, a file system or simple  C malloc() or whatever but it takes care to save data on memory for the system. It is a *critical* shared resource.

**Interface(s)**  
-

**(Optional) Quality/Performance Characteristics**  
-

**(Optional) Directory/File Location>**  
-

**(Optional) Fulfilled Requirements**  
-

**(optional) Open Issues/Problems/Risks**  
-

### ```service_sensors```
**Purpose/Responsibility:**  
Provide values and events coming from the physical world. It is a kind of interaction with the system. Like ```service_IO``` each sensor should have its own task. The described service here is more like a container

**Interface(s)**  
-

**(Optional) Quality/Performance Characteristics**  
-

**(Optional) Directory/File Location>**  
-

**(Optional) Fulfilled Requirements**  
-

**(optional) Open Issues/Problems/Risks**  
-

### ```interrupts```
**Purpose/Responsibility:**  
Container which gathers all interrupt behavior, it is RTOS independent and may preempt full system as its priority is most of the time maximal (except for task of fatal level)



Here you describe \<black box 1> according the the following black box
template:

-   Interface(s), when they are not extracted as separate paragraphs.
    This interfaces may include qualities and performance
    characteristics.

-   (Optional) Quality-/Performance characteristics of the black box,
    e.g.availability, run time behavior, ....

-   (Optional) directory/file location

-   (Optional) Fulfilled requirements (if you need traceability to
    requirements).

-   (Optional) Open issues/problems/risks



### \<Name interface 1> {#__name_interface_1}

### \<Name interface m> {#__name_interface_m}

## Level 2 {#_level_2}

Here you can specify the inner structure of (some) building blocks from
level 1 as white boxes.

You have to decide which building blocks of your system are important
enough to justify such a detailed description. Please prefer relevance
over completeness. Specify important, surprising, risky, complex or
volatile building blocks. Leave out normal, simple, boring or
standardized parts of your system

### White Box *\<building block 1>* {#_white_box_emphasis_building_block_1_emphasis}

...describes the internal structure of *building block 1*.

*\<white box template>*

### White Box *\<building block 2>* {#_white_box_emphasis_building_block_2_emphasis}

*\<white box template>*

...

### White Box *\<building block m>* {#_white_box_emphasis_building_block_m_emphasis}

*\<white box template>*

## Level 3 {#_level_3}

Here you can specify the inner structure of (some) building blocks from
level 2 as white boxes.

When you need more detailed levels of your architecture please copy this
part of arc42 for additional levels.

### White Box \<\_building block x.1\_\> {#_white_box_building_block_x_1}

Specifies the internal structure of *building block x.1*.

*\<white box template>*

### White Box \<\_building block x.2\_\> {#_white_box_building_block_x_2}

*\<white box template>*

### White Box \<\_building block y.1\_\> {#_white_box_building_block_y_1}

*\<white box template>*
