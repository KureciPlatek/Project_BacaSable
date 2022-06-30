# System Scope and Context

The project is limited to a simple program in one hardware device, as cheap as possible because our aim is not to reach fancy performances, but to understand the impact of the quality of our code and architecture.

Our product is a mere simple hardware, which will be programmed and flashed from a simple UNIX/Linux computer, it will have some interactions with the developer, through a serial (UART) communication, but also with a debug/continuous integration server.

 **Optional interfaces**  

An interface with the real physical world may also bring some unexpected inputs to our program. That is why adding one or more sensors may be done

As the need to learn new technologies will surely change in the future, an full list of interfaces can't be fixed. On the contrary, some future hardware/software interfaces are to be considered while describing interfaces to our external world.

***
## Business Context

In the business context, we find the interface to outside world, which are mandatory to fulfill our functional requirements. For example, to apply DevOps development process, we need a unit test interface for the continuous integration server.

**Business context diagram:**  

![Categories of Quality
Requirements](images/Business_context.png)

**list of interfaces and their descriptions:**  

|Interface| purpose | required by | provided by |
|:-:|:-|:-:|:-:|
| Debug / flash | Provide an interface to debug, analyze and flash program on target from a remote host | debugger / flasher | BacaSable |
| Unit test | Interface to execute automatized unit tests on target | continuous integration server  | BacaSable |
| program control / log | Allow human to read log (output from program) or send commands to interact with target while running | developer | BacaSable |
| Analog values | Provide an input of unexpected values from physical world and play with it | BacaSable | Sensor |


***
## Technical Context

We need technical means which allows us to debug, flash and analyze what is happening on our hardware. Those means are described here. Maybe more than one element from business model runs on the same technical mean.  

As our aim is to not to master a special communication protocol or develop a fancy Internet stack, the communications shall remain easy and present on the electronic board/uC/uP.


**Technical context diagram:**  

![Categories of Quality
Requirements](images/Technical_context.png)


**list of interfaces and their descriptions:**  

 - **Debug / flash:**  
 To flash or debug, it is generally a JTAG interface, but depending on target's hardware, it may also be ssh or USB.

 - **Unit test:**  
For unit testing, the server will have to flash on target and get results from debug port. So it is the same interface as **Debug / flash**

 - **program control:**  
To be able to have some interaction with the target, while running, the product need a simple in/out communication which may always work. UART or SPI, may also be I2C, will do.

 - **Analog values:**  
ADC, Analog to Digital Converter over a serial communication. It may be SPI (Quad SPI maybe) or simple GPIOs. It is a board peripheral.

 - **Future use:**  
Many GPIOs will still remain available, as well as potential serial communication and may be used in the future to interface with other boards or new peripherals.

**Resulting table of interfaces:**

| Business interface | Technical mean | in/out | Remarks |
|:-|:-:|:-:|:-|
| Debug / flash | USB | in/out | may change for JTAG. USB for RP2040 uC |
| unit test | USB | in/out | USB for RP2040 uC |
| Commands |  UART over UNIX's ttys | out | Use of terminal or any serial reader program |
| Analog values | ADC over serial (SPI or GPIOs) | in | - |
| future use | GPIOs / serial comm | in/out | _optional_ |
