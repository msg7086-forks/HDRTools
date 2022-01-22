cmake_minimum_required (VERSION 3.22)
set(ASM_DIALECT "_MASM")
set(CMAKE_ASM${ASM_DIALECT}_SOURCE_FILE_EXTENSIONS asm)
set(CMAKE_ASM${ASM_DIALECT}_COMPILER uasm -elf64)

project (hdr-tools CXX ASM${ASM_DIALECT})
file(GLOB C_CODE "*.cpp")
file(GLOB ASM_CODE "*_x64.asm")

add_library(hdr-tools SHARED ${C_CODE} ${ASM_CODE})
set_property(TARGET hdr-tools PROPERTY CXX_STANDARD 17)

find_package(PkgConfig REQUIRED)

pkg_check_modules(AVISYNTH avisynth)
if(AVISYNTH_FOUND)
  include_directories(${AVISYNTH_INCLUDE_DIRS})
endif()

include_directories(.)
