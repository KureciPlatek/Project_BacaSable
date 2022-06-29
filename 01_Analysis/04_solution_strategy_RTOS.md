# Solution Strategy

Gathering input from [RTOS introduction and goals](../00_Requirements_Inputs/01_introduction_and_goals_RTOS.md), we can provide a first, approximation of solution strategy, to fulfill those requirements:

-   Implementation of heavy computing time tasks, at least two, add in the architecture a list of application tasks, whose purpose is undefined, except reply to project's requirements

-   The firmware will be divided in "services" and "tasks", services will take the highest level decomposition of firmware, each service will either be divided in tasks or use them

@TODO: May some tasks be "called upon need", which means they are not periodically called? But only if service or other task need them?

-   All RTOS technology as well as application software (see [introduction and goals](../00_Requirements_Inputs/01_introduction_and_goals.md)) principle we want to understand/improve will be spread among those tasks and services. Those services are like "free containers" which can be created and used. Services will be for application-level software (ex: AI stuff), tasks for technological-level software (ex: ADC polling)

-   There is no particular development process, except for the chosen DevOps, where continuous integration on target with unit tests is desired. Each of the developer has to organize himself with the other to create his own service(s) or task he needs/wants. Or he can use and improve those already developed


@TODO move to solution strategies
### Non RTOS features:
Those features will "fill" the different task's purpose. They are typical services we may meet in RTOS all day life. They may be of interrupt art, heavy computing time, polling art or shared ressource/slow time art.

 - **R3.1.6.1** Service interrupt art: communication SPI, I2C, UART, CAN (not on all uC)
 - **R3.1.6.2** Service heavy computing time art: encryption (AES), FFT or signal processing, artificial intelligence/machine learning
 - **R3.1.6.3** Service polling art: sensors input
 - **R3.1.6.4** Service slow time art: wait for a sub task or peripheral to finish job  

Different code will be developed to show that if one of those is wrongly made, the system can't match the expected requirements. To do that, those different code will compiled in different static libraries and chosen during linking with CMake. Or compiled in dynamic library and program will switch from good to bad to ugly library while running, as human ask for it through an I/O command (like an SPI message which orders program to use bad functions lib instead of good).

@ENDTODO move to solution strategies


### Rejected strategies
@todo

### Documentation
See [Solution Strategy](https://docs.arc42.org/section-4/) in the arc42
documentation.
