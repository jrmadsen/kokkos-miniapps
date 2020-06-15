cmake_minimum_required(VERSION 3.11 FATAL_ERROR)

project(lulesh LANGUAGES C CXX)

include(GNUInstallDirs)

add_option(USE_MPI "Enable MPI" ON)
add_library(lulesh-mpi INTERFACE)
if(USE_MPI)
  find_package(MPI REQUIRED)
  target_compile_definitions(lulesh-mpi INTERFACE USE_MPI=1)
  target_link_libraries(lulesh-mpi INTERFACE MPI::MPI_C MPI::MPI_CXX)
else()
  target_compile_definitions(lulesh-mpi INTERFACE USE_MPI=0)
endif()

add_option(BUILD_LULESH_MINIMAL_CPU "Build minimal cpu version" OFF)
if(BUILD_LULESH_MINIMAL_CPU)
    add_subdirectory(kokkos-minimal-cpu)
endif()
add_subdirectory(kokkos-optimized)
