# Solution Strategy {#section-solution-strategy}

### Contents

A short summary and explanation of the fundamental decisions and
solution strategies, that shape system architecture. It includes

-   technology decisions

-   decisions about the top-level decomposition of the system, e.g.
    usage of an architectural pattern or design pattern

-   decisions on how to achieve key quality goals

-   relevant organizational decisions, e.g. selecting a development
    process or delegating certain tasks to third parties.

### Motivation

The different elements on which the full project will be based are chosen in their qualities of:
 - price
 - Availability
 - match as much features requested as possible

The elements chosen won't be perfect at some requirements will miss. But the most important is to have something light, our aim target is to discover the different technologies principles listed in requirements.

### Form

#### RTOS choice

Many RTOS exists, some are free, other openm source, other closed source, other does not provides all RTOS features (like different schedules like Rate monotonic or Hard/Soft RTOS)

| RTOS | Schedulers | Open source | Free | Supported architectures | Supported Multi core | Size (kBytes) | POSIX |
|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
|FreeRTOS| all | Y | Y | Many | Y | 5-10 | Partially |
|VxWorks | all | N | N | Many | Y |1000-2000| Y |
|ROS | None | Y | Y | Need Ubuntu OS as base. Is a framework, not an RTOS | ? | 1GB | N |
| ThreadX | all | Y | Y | Cortex Ax and Rx | Y | 2-20 | Partially |
| QNX | all | N | N | Many, ask for support | Y | > 50 | Y |

As seen in this array, two RTOS are interesting: FreeRTOS and ThreadX. Both are well supported and are available on many architectures. A huge advantage is also their footprint (less than 24 kBytes) which makes them easier to implement on smaller project.

VxWorks seems to be a reference in the industry and may bring a good experience to our skills, but as it aims too big project for us, its choice is postponed to a later date.

__Choice :__  
With respect of constraints [T1](02_architecture_constraints.md)  
__FreeRTOS or ThreadX__ are good candidates as they offer full RTOS features (hard and soft scheduling, preemptive multi tasking, multi core arch...), they are free of use and seems to have a good community as support. ThreadX is developed by Microsoft and therefore has support.

#### Debugger choice

| Name | Price | Source | Supported arch/uC | gdb |
|:-:|:-:|:-:|:-:|:-:|
| Blackprobe | 65€ | Open | MANY | Y |
| Segger | 400€ | Closed | MANY | Y |
| Lauterbach || |please don't...||
|STLink V3 | 35€ | Closed | STM8/32 only | partially |
| gdb itself | - | open | almost all | - |

Blackprobe presents the advantage to be compact, cheap, open source and provide gdb support as well as the support of many different architectures and uC.  
STLink V3 would also be an interesting choice but is limited to STM8/32 architectures only and has closed source design.  
gdb may be used through some USB or other communication mean to debug program directly on target (for example with the Raspberry Pi)

__Choice :__  
With respect of constraints [O2](02_architecture_constraints.md)  
If only gdb may be used, then __gdb__. Otherwise, go for an architecture supported either by STLink or __BlackProbe__.

#### Hardware target choice

The hardware target choice is motivated by one hardware filling most of the wanted characteristics. As the two previous arrays present Blackprobe as a good debugger and FreeRTOS or ThreadX as a good RTOS choice, all three of them will be added into hardware choice array

| Board | Price | Architecture | Constructor |  Blackprobe | STLink V3 |  FreeRTOS | ThreadX | DSP | Multi-core | Memory | Others |
|-|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:|
| NUCLEO-F439ZI|22€ | STM32 Cortex-M4 | ST | Y | Y | Y (with GCC) | Y (with GCC) | Y | N | 2M | FPU, ADC, Crypto
| NUCLEO-F756ZG|22€| STM32 Cortex-M7 | ST | Y | Y |Y (with GCC)|Y (with gcc)| Y | N | 1M	| FPU, L1 cache, HW Crypto |
|NUCLEO-H753ZI| 26€ | STM32 Cortex-M7 | ST | Y | Y | Y (with gcc) | Y (with GCC)| Y | N |	2M	| DP-FPU L1 cache, ADC, DAC, HW Crypto |
|NUCLEO-H755ZI-Q|28€|STM32 Cortex-M7/M4 | ST |	Y | Y| Y (with gcc) |Y (with GCC) |Y | (Y) asymmetric | 2M |DP-FPU L1 cache, ADC, DAC,HW Crypto |
|NUCLEO-WL55JC |41€|STM32 Cortex-M4/M0+ | ST | Y|Y|Y (with gcc) |Y (with GCC)| Y |  (Y) asymmetric | 256k | Ultra low power, DSP, AES-256, LoRa, GFSK, MSK, BPSK, Bluetooth LE |
| P-NUCLEO-WB55 | 41€ | STM32WB55 Cortex-M4/M0+ | ST | Y|Y|Y (with gcc) | Y (with GCC) | Y | (Y) asymmetric | 1M |	Ultra low power, AES-256 crypto, Bluetooth LE, Thread comm |
| Jetson Nano-Entwicklerkit | 250€ | Cortex-A57 | Nvidia | N | N | N | N | ? | 4  | 16G | GPU, L1 cache, Ethernet |
| Raspberry Pi 4 | 67€ | Broadcom Cortex-A72 | Raspberry | N (but gdb) | N (but gdb)| Y (but complex), better a RTLinux | N | Y | 4 | Big |WLAN, Bluetooth 5.0, high perf computer arch
| Raspberry Pico | 5€ | RP2040 Dual core Cortex M0+ | Raspberry | N (but gdb) | N | Y (with gcc) | Y (with gcc) |N| 2 | 16M | SPI, I2C, C/C++ lib for RP2040 |

Raspberry Pi target has a huge advantage to be available for many of developers (who don't have its Raspberry ?! Witch hunt will start ), and as Linux is respects UNIX/POSIX standards, a full implementation of a multi thread, multi core project already may be done on this target.

A nucleo board presents nevertheless a good price/features ratio for pure embedded and hard RTOS purposes (FreeRTOS and ThreadX). They are also programmable as an external target through a cheap BlackProbe debugger which could be controlled by a Jenkins server.

__Choice :__  
With respect of constraints [O2](02_architecture_constraints.md), [T2](02_architecture_constraints.md), [3](02_architecture_constraints.md), [T4](02_architecture_constraints.md) and [T5](02_architecture_constraints.md) (have a double core)  
The __Raspberry Pico__ will be used as hardware target, as it costs almost nothing, is simple and provides a double core Cortex-M0+

### Rejected strategies
#### Rejected RTOS
 - VxWorks and QNX will not be used as they are commercial use and need a license
 - As ROS is not an RTOS but a framework, it won't be used as scheduler

#### Debugger
 - Lauterbach is simply too expensive
 - Segger is also very expensive, and in the case of using RP2040 uC, it makes not many sense
 - Blackprobe is more oriented for STM32 uC, it may be used in the future as it is open source and is not expensive

#### Hardware target
 - Nvidia Jetson will not be used, too expensive and too big for a sandbox project
 - NUCLEO boards may be used in future if chosen target meets limitations

### Documentation
See [Solution Strategy](https://docs.arc42.org/section-4/) in the arc42
documentation.
