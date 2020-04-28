add_library(cvmix_objects OBJECT .)
set_property( TARGET cvmix_objects PROPERTY FOLDER shared )

target_sources( cvmix_objects PRIVATE
   cvmix_kinds_and_types.F90
   cvmix_background.F90
   cvmix_convection.F90
   cvmix_ddiff.F90
   cvmix_kpp.F90
   cvmix_math.F90
   cvmix_put_get.F90
   cvmix_shear.F90
   cvmix_tidal.F90
   cvmix_utils.F90
)
