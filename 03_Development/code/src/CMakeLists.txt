cmake_minimum_required(VERSION 3.13)

# Used langages: C, C++ and assembler.
message("Project BacaSable - have fun with DevOps, embedded dev, RTOS and AI")

# Set pico environment path. @todo: use bash environment variable doesn't work yet
set(PICO_SDK_PATH /opt/pico-sdk)

# Include Raspberry Pico specific cmake - MUST BE CALLED BEFORE project() FUNCTION!
include(${PICO_SDK_PATH}/external/pico_sdk_import.cmake)

# Set Project name
project(bacaSable VERSION 0.1 LANGUAGES C CXX ASM)

# Set C and C++ standards
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Set gcc compiling options and flags
set(CMAKE_C_FLAGS_PROFILE "-Wall")

# Init pico development kit (cmake call)
pico_sdk_init()

add_executable(${PROJECT_NAME} main.c)

#@todo
pico_add_extra_outputs(${PROJECT_NAME})

target_link_libraries(${PROJECT_NAME} pico_stdlib)

#Pico SDK specific, configure IO
pico_enable_stdio_usb(${PROJECT_NAME} 1)
pico_enable_stdio_uart(${PROJECT_NAME} 0)

message("Generate of RaspPico makefiles done")
