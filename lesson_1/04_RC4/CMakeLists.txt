set(PROJECT "RC4")
project(${PROJECT} CXX)

cmake_minimum_required(VERSION 3.5)
FIND_PACKAGE(OpenMP REQUIRED)

message("\nTest on cmake v" ${CMAKE_VERSION} "  System: " ${CMAKE_SYSTEM} "\n")

# ------------------------------------------------------------------------------
# CHECK C++ 14

include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++14" COMPILER_SUPPORTS_CXX14)
if(COMPILER_SUPPORTS_CXX14)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14")
else()
    message(FATAL_ERROR "Compiler ${CMAKE_CXX_COMPILER} has no C++14 support.")
endif()

# ------------------------------------------------------------------
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")

#set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS}
#                            ${OpenMP_EXE_LINKER_FLAGS}")

add_compile_options("-O3")
add_executable(rc4 ${PROJECT_SOURCE_DIR}/RC4.cpp)