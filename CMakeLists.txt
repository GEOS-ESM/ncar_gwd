esma_set_this()

set (srcs
  linear_1d_operators.F90
  interpolate_data.F90
  vdiff_lu_solver.F90
  coords_1d.F90
  gw_utils.F90
  gw_common.F90
  gw_convect.F90
  gw_rdg.F90
  gw_oro.F90
  gw_drag.F90
  )

esma_add_library (${this}
  SRCS ${srcs}
  DEPENDENCIES MAPL esmf NetCDF::NetCDF_Fortran
  )

# CMake has an OpenMP issue with NAG Fortran: https://gitlab.kitware.com/cmake/cmake/-/issues/21280
if (NOT CMAKE_Fortran_COMPILER_ID MATCHES "NAG")
   target_link_libraries(${this} PRIVATE OpenMP::OpenMP_Fortran)
endif ()
