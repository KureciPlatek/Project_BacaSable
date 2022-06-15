# Developing on Raspberry Pico env

**Mandatory elements/progs for developing on Pico:**  
To do some development on this project or just use it, you may need to execute the following steps if you never made it:
1.	Install git
2.	Install CMake
3.	Install GNU Arm Embedded Toolchain
4.	Install and configure Raspberry Pico SDK


## Setup on Linux environment

### 1. Install git
> $ sudo apt-get install git

### 2. Install CMake
> $ sudo apt-get install cmake

### 3. Install ARM embedded toolchain

1. **Step one**  
Download the arm compiler suite from [ARM official website](https://developer.arm.com/downloads/-/gnu-rm). You will get a gcc-arm-none-eabi-x.x.x-xxx64-linux.tar.bz2 file. It contains the full   
Go to the folder where your file was downloaded, the x are the last version, date and architecture you need for your Linux arch. For me it was the x86_64.  

2. **Step two**  
The second step is to install all this compiler suite somewhere you want. It is important to choose it well because you will need top add it to your PATH.
> $ sudo tar xjf gcc-arm-none-eabi-10.3-2021.10-x86_64-linux.tar.bz2 -C /your/path/

3. **Step three**  
Third step: add compiler suite to PATH:
> $ echo 'export PATH=$PATH:/your/path/gcc-arm-none-eabi/bin' | sudo tee -a /etc/profile.d/gcc-arm-none-eabi.sh


### 4. Install and configure Raspberry ```pico-sdk```

1. **Step one get pico-sdk**  
Clone PICO-SDK project from github in /opt/pico-sdk/ but you may give another place:
> $ sudo git clone https://github.com/raspberrypi/pico-sdk.git /opt/pico-sdk  


2. **Step two Initialize sub-modules**  
Just do it, be careful with path
> $ sudo git -C /opt/pico-sdk submodule update --init

3. **Step three add it to PATH**  
Project's cmake files will use the ```$ENV{PICO_SDK_PATH}``` variable to get pico-sdk libraries. Make sure your PATH has the link to the pico-sdk, otherwise CMake will not work.  
> $ echo 'export PICO_SDK_PATH=/opt/pico-sdk' | sudo tee -a /etc/profile.d/pico-sdk.sh


## Setup on MacOS
@todo

## Compile and load program on target

### Compile
To compile, it is the same process as with usual CMake project, just a small last step need to be done.  
After you generated the compiling scripts with CMake, just make won't work, do instead:
 > $ make -j$(nproc)

It will generate a lot of files, elf files and a .uf2 file which will be our executable to be loaded on target.

### Flash
To flash and execute, Raspberry Pico behaves like an USB mass storage device you need to mount. After mounted, you can copy the executable.uf2 file on it, it will execute by itself automatically.

**Find the Raspberry Pico:**  
Either on the file explorer if mounted, or on terminal:
> $ sudo blkid -o list | grep RPI-RP2

Output:
> /dev/sdb1  vfat    RPI-RP2  (not mounted)  0034-04C4

Then create a directory for it to be mounted and mount it:
> $ sudo mkdir /mnt/pico  
> $ sudo mount /dev/sdb1 /mnt/pico

Be careful with the sdb1 port! It may be another name.

You should then find the following files in the RPI-RP2 directory:  
> INDEX.HTM  INFO_UF2.TXT

**Load executable on target**  
Copy program on target and flush memory buffer to the storage device:

> $ sudo cp myapp.uf2 /mnt/pico  
> $ sudo sync

**Check output**  
The stdio of Raspberry Pico can be found on the /dev/ttyACM0 port.  
To read it, either do it with `minicom` or `screen` program, baudrate is 115200 bauds.

> $ sudo screen /dev/ttyACM0 115200
