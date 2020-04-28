# CVMix library sources
add_subdirectory( shared )

#configure_file(${CMAKE_CURRENT_SOURCE_DIR}/cvmix_version.F90.in ${CMAKE_CURRENT_BINARY_DIR}/cvmix_version.F90)

if(CVMIX_BUILD_DRIVER)

   add_library(cvmix_io STATIC .)
   set_property( TARGET cvmix_io PROPERTY FOLDER drivers )
   target_sources( cvmix_io PRIVATE
      cvmix_io.F90
   )
   target_link_libraries(cvmix_io PRIVATE cvmix_static)

   add_subdirectory( drivers )

endif()
