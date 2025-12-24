cmake_minimum_required(VERSION 3.30)
project(acpica C)

set(ACPICA_DIR ${CMAKE_CURRENT_LIST_DIR})

file(GLOB_RECURSE ACPICA_SOURCES
    ${ACPICA_DIR}/source/*.c
)

add_library(acpica STATIC ${ACPICA_SOURCES})

target_include_directories(acpica
    PRIVATE
        ${ACPICA_DIR}/source/include
)

target_compile_options(acpica
    PRIVATE
        -m64
        -O2
        -g0
        -fdata-sections
        -ffunction-sections
        -fno-stack-protector
        -fno-builtin
        -fno-omit-frame-pointer
        -mno-red-zone
        -fno-pic
        -fno-pie
)

target_compile_definitions(acpica
    PRIVATE
        ACPI_USE_SYSTEM_CLIB
)
