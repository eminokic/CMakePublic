cmake_minimum_required(VERSION 3.13.4)
project(CMakePublic)

add_library(CMakePublic cmake_public.cpp)

#include header file
target_include_directories (CMakePublic PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

message("Processing CMakeLists.txt")
