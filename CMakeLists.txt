
cmake_minimum_required(VERSION 3.8.2)

set(ENV{ARDUINO_SDK_PATH} "/home/yura/arduino-sdk/arduino-1.8.7")

set(CMAKE_TOOLCHAIN_FILE
    "${CMAKE_CURRENT_SOURCE_DIR}/Arduino-CMake-NG/cmake/Arduino-Toolchain.cmake")

project(gizmo_relay_box LANGUAGES C CXX ASM)


arduino_cmake_project(gizmo_relay_box BOARD_NAME uno)

add_arduino_executable(gizmo_relay_box src/main.cpp)

find_arduino_library(SPI_lib SPI)
link_arduino_library(gizmo_relay_box SPI_lib)

add_arduino_library(RF24 RF24/RF24.cpp)
link_arduino_library(RF24 SPI_lib)
target_include_directories(RF24 PUBLIC RF24)
link_arduino_library(gizmo_relay_box RF24)


set_target_upload_port(gizmo_relay_box /dev/ttyUSB0)

