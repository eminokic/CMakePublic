cmake_minimum_required(VERSION 3.13.4)
project(CMakePublic VERSION 1.0.0 LANGUAGES CXX)

add_library(CMakePublic cmake_public.cpp)

#include header file
target_include_directories (CMakePublic PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>)

install(TARGETS CMakePublic
    EXPORT CMakePublic-targets
    PUBLIC_HEADER DESTINATION include
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
    RUNTIME DESTINATION bin)

install(EXPORT CMakePublic-targets
    NAMESPACE CMakePublic::
    FILE CMakePublicConfig.cmake
    DESTINATION lib/cmake/CMakePublic)

message("Processing CMakeLists.txt")
