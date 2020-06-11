cmake_minimum_required(VERSION 3.11 FATAL_ERROR)

project(kokkos-miniapps LANGUAGES C CXX)

set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake/Modules ${CMAKE_MODULE_PATH})

include(GNUInstallDirs)
include(MiniappUtilities)

find_package(Kokkos QUIET)

set(AVAILABLE_PROJECTS lulesh ExaMiniMD SNAP hpcg miniAero miniFE miniMD)
set(PROJECTS "lulesh" CACHE STRING "Projects to build")
set_property(CACHE PROJECTS PROPERTY STRINGS "${AVAILABLE_PROJECTS}")

add_feature(PROJECTS "Projects to build")

if("${CMAKE_BUILD_TYPE}" STREQUAL "")
    set(CMAKE_BUILD_TYPE "Release" CACHE STRING "CMake build type" FORCE)
endif()

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR})
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR})
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_BINARY_DIR})

add_subproject(lulesh       DIRECTORY lulesh-2.0)
add_subproject(ExaMiniMD    SUBMODULE)
add_subproject(SNAP         SUBMODULE)
add_subproject(hpcg         SUBMODULE)
add_subproject(miniAero     SUBMODULE)
add_subproject(miniFE       SUBMODULE)
add_subproject(miniMD       SUBMODULE)


print_features()
