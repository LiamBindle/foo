cmake_minimum_required (VERSION 3.13)

project (GCHP_DEPS
  VERSION 0.0.0
  LANGUAGES Fortran CXX C
)

# Make ESMA's and ecbuild's modules available
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/ESMA_cmake ${CMAKE_CURRENT_SOURCE_DIR}/ecbuild/cmake)

# Import ESMA's cmake macros
include(esma-community)

# Declare ecbuild project
ecbuild_declare_project()

# Find MPI
find_package(MPI REQUIRED COMPONENTS C CXX Fortran)

# Add MPI compiler flags
set(CMAKE_Fortran_FLAGS ${CMAKE_Fortran_FLAGS} ${MPI_Fortran_COMPILE_OPTIONS})
set(CMAKE_C_FLAGS ${CMAKE_C_FLAGS} ${MPI_C_COMPILE_OPTIONS})
set(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS} ${MPI_CXX_COMPILE_OPTIONS})
add_definitions(${MPI_Fortran_COMPILE_DEFINITIONS} ${MPI_C_COMPILE_DEFINITIONS} ${MPI_CXX_COMPILE_DEFINITIONS})
include_directories(${MPI_Fortran_INCLUDE_DIRS} ${MPI_C_INCLUDE_DIRS} ${MPI_CXX_INCLUDE_DIRS})

# Pretend LaTeX isn't found so that dependencies like ImageMagick aren't necessary
set(LATEX_FOUND FALSE)

add_subdirectory(MAPL EXCLUDE_FROM_ALL)         # MAPL_Base

set(NO_F2PY TRUE)
add_subdirectory(GMAO_Shared EXCLUDE_FROM_ALL)  # GEOS_Shared GMAO_hermes

set(FV_PRECISION R8)
add_subdirectory(GEOSgcm_GridComp EXCLUDE_FROM_ALL)
