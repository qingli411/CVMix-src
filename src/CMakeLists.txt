cmake_minimum_required(VERSION 3.1)

# Create main project
project(cvmix Fortran)

# Set default installation prefix
if(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)
    SET(CMAKE_INSTALL_PREFIX ${PROJECT_SOURCE_DIR}/../ CACHE PATH "Directory to install CVMix in" FORCE)
endif(CMAKE_INSTALL_PREFIX_INITIALIZED_TO_DEFAULT)

# CVMix library source files
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

# Install CVMix library
install(TARGETS cvmix DESTINATION lib)
install(DIRECTORY ${CMAKE_Fortran_MODULE_DIRECTORY}/ DESTINATION include)

# Build CVMix executable for tests
if(CVMix_BUILD_TEST)
    # CVMix driver source files
    set(CVMix_DRIVERS_SOURCE_DIR ${PROJECT_SOURCE_DIR}/drivers)

    # Build CVMix executable
    add_executable(cvmix_exe
        ${PROJECT_SOURCE_DIR}/cvmix_driver.F90
        ${PROJECT_SOURCE_DIR}/cvmix_io.F90
        ${CVMix_DRIVERS_SOURCE_DIR}/cvmix_bgrnd_BL.F90
        ${CVMix_DRIVERS_SOURCE_DIR}/cvmix_ddiff_drv.F90
        ${CVMix_DRIVERS_SOURCE_DIR}/cvmix_kpp_drv.F90
        ${CVMix_DRIVERS_SOURCE_DIR}/cvmix_shear_drv.F90
        ${CVMix_DRIVERS_SOURCE_DIR}/cvmix_tidal_Simmons.F90
    )
    set_property(TARGET cvmix_exe PROPERTY RUNTIME_OUTPUT_NAME "cvmix")
    target_link_libraries(cvmix_exe cvmix)

    # Install CVMix executable
    install(TARGETS cvmix_exe DESTINATION bin)
endif(CVMix_BUILD_TEST)

