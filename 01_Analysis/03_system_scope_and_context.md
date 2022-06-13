# System Scope and Context {#section-system-scope-and-context}

### Contents

The project is limited to a simple program in one hardware device, as cheap as possible because our aim is not to reach fancy performances, but to understand the impact of the quality of our code and of our architecture.

Our product is a mere simple hardware, which will be programmed and flashed from a simple UNIX/Linux computer, it will have some interactions with ourselves, through a simple communication, but also with a debug/continuous integration server.

An interface with the real physical world may also bring some unexpected behavior to our program. That is why adding one or more sensors will be done

### Motivation

The domain interfaces and technical interfaces to communication partners
are among your system's most critical aspects. Make sure that you
completely understand them.  
-> @todo

## Business Context {#_business_context}

**Contents**  
There is no special business context as our aim is to show some technical skills instead of developing a business model and win money

**Motivation**  
*none*  

**Form**  
*none*  


## Technical Context {#_technical_context}

### Contents

We need communication means which allows us to debug, flash and analyze what is happening on our hardware.  
To be able to have some interaction with the target, while running, the product need a simple in/out communication which may always work.  
Finally, a "close to hardware" interface is also wished, because we want to build some embedded, hardware-close (almost analog) real-time OS.

### Motivation

There are 4 main communication interfaces:
 - ssh for flashing, debugging and analysis of code
 - UART or SPI, may also be I2C, a simple embedded communication mean for communication with external world, it will be used by human user
 - ADC, Analog to Digital Converter as we seek to have some random info which need to be periodically polled

As our aim is to not to master a special communication protocol or develop a fancy Internet stack, the communications are mainly easy and present on every electronic board/uC/uP.

### Form

*Technical context diagram:*  

![Categories of Quality
Requirements](images/Technical_context.png)


*list of interfaces and their descriptions:*  

|Interface| purpose | required by | provided by | Technical mean | in/out |
|:-:|:-|:-:|:-:|:-:|:-:|
|Debug | Provide an interface to debug target from a remote host | dbg server | BacaSable | ssh? | in/out |
|unit test | Interface to execute automatized unit tests on target with a continuous integration server | DevOps | BacaSable | ssh? | in/out |
| Commands | Allow human to read info or send commands to target while running | human | BacaSable | UART or SPI | out |
| Analog values | Provide values coming from physical world and play with it | BacaSable | Sensor | ADC | in |
