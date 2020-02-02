cmake_minimum_required(VERSION 3.1)

# Create main project
project (cvmix Fortran)

# Set default installation prefix
IF(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
    SET(CMAKE_INSTALL_PREFIX ${PROJECT_SOURCE_DIR}/../ CACHE PATH "Directory to install CVMix in" FORCE)
ENDIF(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)

# CVMix source files
set(CVMix_SHARED_SOURCE_DIR ${PROJECT_SOURCE_DIR}/shared)
set(SOURCES
    ${CVMix_SHARED_SOURCE_DIR}/cvmix_kinds_and_types.F90
    ${CVMix_SHARED_SOURCE_DIR}/cvmix_background.F90
    ${CVMix_SHARED_SOURCE_DIR}/cvmix_convection.F90
    ${CVMix_SHARED_SOURCE_DIR}/cvmix_ddiff.F90
    ${CVMix_SHARED_SOURCE_DIR}/cvmix_kpp.F90
    ${CVMix_SHARED_SOURCE_DIR}/cvmix_math.F90
    ${CVMix_SHARED_SOURCE_DIR}/cvmix_put_get.F90
    ${CVMix_SHARED_SOURCE_DIR}/cvmix_shear.F90
    ${CVMix_SHARED_SOURCE_DIR}/cvmix_tidal.F90
    ${CVMix_SHARED_SOURCE_DIR}/cvmix_utils.F90
)

# Set directory for .mod files
set(CMAKE_Fortran_MODULE_DIRECTORY ${PROJECT_SOURCE_DIR}/../include)

# Build CVMix library
add_library(cvmix STATIC ${SOURCES})

# Install
install(TARGETS cvmix DESTINATION lib)
install(DIRECTORY ${CMAKE_Fortran_MODULE_DIRECTORY}/ DESTINATION include)
