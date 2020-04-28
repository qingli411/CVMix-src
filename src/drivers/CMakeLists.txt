add_library(cvmix_drivers STATIC .)
set_property( TARGET cvmix_drivers PROPERTY FOLDER drivers )

target_sources( cvmix_drivers PRIVATE
   cvmix_bgrnd_BL.F90
   cvmix_ddiff_drv.F90
   cvmix_kpp_drv.F90
   cvmix_shear_drv.F90
   cvmix_tidal_Simmons.F90
)
target_link_libraries( cvmix_drivers PRIVATE cvmix_io )

