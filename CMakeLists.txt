set(CMAKE_TOOLCHAIN_FILE "${DEVKITPRO}/cmake/3DS.cmake")
list(APPEND CMAKE_PREFIX_PATH "${DEVKITPRO}/portlibs/3ds/lib/pkgconfig/")
cmake_minimum_required(VERSION 3.24)
project(matrix-3ds-sdk)

add_library(matrix-3ds-sdk source/matrixclient.cpp source/memorystore.cpp source/util.cpp)
find_package(PkgConfig REQUIRED)
pkg_check_modules(jansson REQUIRED IMPORTED_TARGET jansson)

# libtool usage forcing this little hack
file(READ "${DEVKITPRO}/portlibs/3ds/lib/libcurl.la" contents)
if (contents MATCHES "dependency_libs *= *'([^']*)'")
    string(STRIP "${CMAKE_MATCH_1}" deps)
    string(REGEX REPLACE " +" ";" deps "${deps}")
    target_link_libraries(matrix-3ds-sdk PRIVATE curl PkgConfig::jansson ${deps})
endif()

target_include_directories(matrix-3ds-sdk PUBLIC source include "${DEVKITPRO}/portlibs/3ds/include/")
