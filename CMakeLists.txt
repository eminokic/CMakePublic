#[[
 All CMake projects should start with a line declaring the minimum version of
 CMake required to build the project and a line declaring the project. The
 former ensures that the user's CMake supports all of the features required to
 build the project. The latter is required by CMake for each project.
#]]
cmake_minimum_required(VERSION 3.13.4)
project(CMakePublic VERSION 1.0.0 LANGUAGES CXX)

#[[
 When writing your own CMakeLists.txt it is strongly recommended that you use
 the GNUInstallDirs module to get the installation directory names appropriate
 for the present operating system (e.g. lib, include, bin)
#]]
include(GNUInstallDirs)

#[[
 CMake best practices use lowercase target names. For the purposes of this file
 we set our project's target's name to a lowercase version of the project's name
 (i.e., ${target_name} == cmakepublic)
#]]
string(TOLOWER "${PROJECT_NAME}" target_name)

#[[
 N.B. When adding a library it is recommended that you do not specify the
 library type (shared, static, or module) as this allows the user to control the
 type via the BUILD_SHARED_LIBS CMake variable (default is static).
#]]
add_library("${target_name}" src/cmake_public.cpp)

#[[
 N.B. In order for CMake to install your header files, it is not enough to tell
 CMake which directories contain your project's public header files, you also
 need to add those files to the PUBLIC_HEADER property of the target. Conversely
 telling CMake the path to the headers is not enough for it to figure out the
 include directories to provide the compiler and users must also set the
 target's include directories via target_include_directories.
#]]
set(target_inc_dir "${CMAKE_CURRENT_SOURCE_DIR}/include")
target_include_directories(
    "${target_name}" PUBLIC $<BUILD_INTERFACE:${target_inc_dir}>
                            $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>
)
set_target_properties(
    "${target_name}" PROPERTIES
    PUBLIC_HEADER "${target_inc_dir}/cmake_public.hpp"
)


install(
    TARGETS "${target_name}"
    EXPORT "${PROJECT_NAME}-targets"
    PUBLIC_HEADER DESTINATION "${CMAKE_INSTALL_FULL_INCLUDEDIR}"
    ARCHIVE DESTINATION "${CMAKE_INSTALL_FULL_LIBDIR}"
    LIBRARY DESTINATION "${CMAKE_INSTALL_FULL_LIBDIR}"
    RUNTIME DESTINATION "${CMAKE_INSTALL_FULL_BINDIR}"
)

install(
    EXPORT "${PROJECT_NAME}-targets"
    NAMESPACE "${PROJECT_NAME}::"
    FILE "${PROJECT_NAME}Config.cmake"
    DESTINATION "${CMAKE_INSTALL_FULL_LIBDIR}/cmake"
)
