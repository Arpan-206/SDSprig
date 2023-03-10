# Generated Cmake Pico project file

cmake_minimum_required(VERSION 3.13)

set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Initialise pico_sdk from installed location
# (note this can come from environment, CMake cache etc)
set(PICO_SDK_PATH "/Users/arpanpandey/raspberrypi/pico-sdk")

set(PICO_BOARD pico CACHE STRING "Board type")

# Pull in Raspberry Pi Pico SDK (must be before project)
include(pico_sdk_import.cmake)

project(SDSprig C CXX ASM)

# Initialise the Raspberry Pi Pico SDK
pico_sdk_init()

# Add executable. Default name is the project name, version 0.1

add_executable(SDSprig SDSprig.c hw_config.c)

pico_set_program_name(SDSprig "SDSprig")
pico_set_program_version(SDSprig "0.1")

pico_enable_stdio_uart(SDSprig 0)
pico_enable_stdio_usb(SDSprig 1)

add_subdirectory(lib/no-OS-FatFS-SD-SPI-RPi-Pico/FatFs_SPI build)

# Add the standard library to the build
target_link_libraries(SDSprig
        pico_stdlib
        FatFs_SPI)

# Add the standard include files to the build
target_include_directories(SDSprig PRIVATE
  ${CMAKE_CURRENT_LIST_DIR}
  ${CMAKE_CURRENT_LIST_DIR}/.. # for our common lwipopts or any other standard includes, if required
)


pico_add_extra_outputs(SDSprig)

