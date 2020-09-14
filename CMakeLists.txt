cmake_minimum_required(VERSION 3.13.4)
SET(CMAKE_INSTALL_PREFIX /Users/ally/CMaizeExamples/CMakePublic)
project(CMakePublic VERSION 1.0.0 LANGUAGES CXX)

#message("install prefix ${CMAKE_INSTALL_PREFIX}")

add_library(${PROJECT_NAME} cmake_public.cpp)

include(GNUInstallDirs)

#include header file
#target_include_directories(mylib PUBLIC
#  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include/mylib>
#  $<INSTALL_INTERFACE:include/mylib>  # <prefix>/include/mylib
#)

#investigate this more!!!!
target_include_directories (${PROJECT_NAME} PUBLIC 
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  #$<INSTALL_INTERFACE:include/$PROJECT_NAME
)

#install the target in the install tree
install(TARGETS ${PROJECT_NAME}
    EXPORT ${PROJECT_NAME}-targets
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_INCLUDEDIR}
    ARCHIVE DESTINATION ${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}
    LIBRARY DESTINATION ${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}
    RUNTIME DESTINATION ${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_BINDIR}
)


install(EXPORT ${PROJECT_NAME}-targets
    NAMESPACE ${PROJECT_NAME}::
    FILE ${PROJECT_NAME}Config.cmake
    DESTINATION ${CMAKE_INSTALL_PREFIX}/${CMAKE_INSTALL_LIBDIR}
)

message("Processing CMakeLists.txt")
