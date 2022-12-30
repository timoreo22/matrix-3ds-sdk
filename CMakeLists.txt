set(CMAKE_TOOLCHAIN_FILE /opt/devkitpro/cmake/3DS.cmake)
cmake_minimum_required(VERSION 3.24)
project(matrix-3ds-sdk)

add_library(matrix-3ds-sdk source/matrixclient.cpp source/memorystore.cpp source/util.cpp)
target_include_directories(matrix-3ds-sdk PUBLIC source include /opt/devkitpro/portlibs/3ds/include/)