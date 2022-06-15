cmake_minimum_required(VERSION 3.13)

# Used langages: C, C++ and assembler.
message("Project BacaSable - have fun with DevOps, embedded dev, RTOS and AI")
message("Working directory:  ${CMAKE_SOURCE_DIR}")

# Include Raspberry Pico specific cmake
include($ENV{PICO_SDK_PATH}/external/pico_sdk_import.cmake)

project(bacaSable VERSION 0.1 LANGUAGES C CXX ASM)

# Enable testing with CTest
enable_testing()

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Set all created library to SHARED ot STATIC.
set(BUILD_SHARED_LIBS YES)
# Set drivers directory
set(DRIVERS_DIR ${CMAKE_SOURCE_DIR}/drivers)
# Set Applicative software directory
set(APPSOFT_DIR ${CMAKE_SOURCE_DIR}/AppSoftware)
# Set gcc compiling options and flags
set(CMAKE_C_FLAGS_PROFILE "-Wall -g -O2" "CACHE STRING")
# Set unit test directory
set(UNITTEST_DIR ${CMAKE_SOURCE_DIR}/unit_test)

# Init pico development kit (cmake call)
pico_sdk_init()

#add_executable(${PROJECT_NAME} main.c)

add_executable(${PROJECT_NAME}
    ${UNITTEST_DIR}/ut_torque_computing.c
    ${DRIVERS_DIR}/adc_driver/adc_driver.c
    ${DRIVERS_DIR}/error_led/error_led.c
    ${DRIVERS_DIR}/sensor_driver/sensor.c
    ${APPSOFT_DIR}/torque_computing.c
)

#@todo
pico_add_extra_outputs(${PROJECT_NAME})

target_link_libraries(${PROJECT_NAME} pico_stdlib m)

#Pico SDK specific, configure IO
pico_enable_stdio_usb(${PROJECT_NAME} 1)
pico_enable_stdio_uart(${PROJECT_NAME} 0)

message("Generate of Unix makefiles done")
