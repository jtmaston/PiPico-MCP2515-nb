cmake_minimum_required(VERSION 3.8)

# initialize the SDK based on PICO_SDK_PATH
# note: this must happen before project()
include(pico-sdk/pico_sdk_init.cmake)


project(MCPPico VERSION 0.1 LANGUAGES CXX C ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# initialize the Raspberry Pi Pico SDK
pico_sdk_init()

# rest of your project
add_library(PicoMCP STATIC
    ${PROJECT_SOURCE_DIR}/src/MCP2515.cpp
    ${PROJECT_SOURCE_DIR}/src/CANPacket.cpp
    ${PROJECT_SOURCE_DIR}/src/Utilities.cpp
)


set_target_properties(PicoMCP PROPERTIES
    PUBLIC_HEADER "${PROJECT_SOURCE_DIR}/src/MCP2515.h"
)
target_include_directories(PicoMCP PRIVATE ${PROJECT_SOURCE_DIR}/src)

target_link_libraries(PicoMCP
  pico_stdlib
  pico_multicore
  hardware_spi
)


#target_compile_features(PicoMCP
#    PUBLIC
#    cxx_attributes
#    cxx_defaulted_functions
#    cxx_deleted_functions
#    cxx_final
#)