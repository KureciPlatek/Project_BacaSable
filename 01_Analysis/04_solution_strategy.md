# Solution Strategy {#section-solution-strategy}

**Contents**

A short summary and explanation of the fundamental decisions and
solution strategies, that shape system architecture. It includes

-   technology decisions

-   decisions about the top-level decomposition of the system, e.g.
    usage of an architectural pattern or design pattern

-   decisions on how to achieve key quality goals

-   relevant organizational decisions, e.g. selecting a development
    process or delegating certain tasks to third parties.

**Motivation**

These decisions form the cornerstones for your architecture. They are
the foundation for many other detailed decisions or implementation
rules.

**Form**

Keep the explanations of such key decisions short.

Motivate what was decided and why it was decided that way, based upon
problem statement, quality goals and key constraints. Refer to details
in the following sections.

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

#### Debugger choice

| Name | Price | Source | Supported arch/uC | gdb |
|:-:|:-:|:-:|:-:|:-:|
| Blackprobe | 65€ | Open | MANY | Y |
| Segger | 400€ | Closed | MANY | Y |
| Lauterbach || |please don't...||
|STLink V3 | 35€ | Closed | STM8/32 only | partially |

Blackprobe presents the advantage to be compact, cheap, open source and provide gdb support as well as the support of many different architectures and uC.
STLink V3 would also be an interesting choice but is limited to STM8/32 architectures only and has closed source design.

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

Raspberry Pi target has a huge advantage to be available for many of developers (who don't have its Raspberry ?! Witch hunt will start ), and as Linux is respects UNIX/POSIX standards, a full implementation of a multi thread, multi core project already may be done on this target.

A nucleo board presents nevertheless a good price/features ratio for pure embedded and hard RTOS purposes (FreeRTOS and ThreadX). They are also programmable as an external target through a cheap BlackProbe debugger which could be controlled by a Jenkins server.

**Rejected strategies**



**Documentation**
See [Solution Strategy](https://docs.arc42.org/section-4/) in the arc42
documentation.
