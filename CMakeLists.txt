cmake_minimum_required (VERSION 3.13)

project (
  GCHP_DEPS
  VERSION 0.0.0
  LANGUAGES Fortran CXX C)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/ESMA_cmake ${CMAKE_CURRENT_SOURCE_DIR}/ecbuild/cmake)
include(esma)

set(EXCLUDE_FROM_ALL TRUE)
add_subdirectory(MAPL)

