cmake_minimum_required(VERSION 3.11 FATAL_ERROR)

project(lulesh-optimized LANGUAGES C CXX)

find_package(Kokkos REQUIRED)
file(GLOB sources ${PROJECT_SOURCE_DIR}/*.cc)
add_executable(${PROJECT_NAME} ${sources})
target_include_directories(${PROJECT_NAME} PRIVATE ${PROJECT_SOURCE_DIR}/includes)
target_link_libraries(${PROJECT_NAME} PRIVATE Kokkos::kokkos lulesh-mpi)
install(TARGETS ${PROJECT_NAME} DESTINATION ${CMAKE_INSTALL_BINDIR})
