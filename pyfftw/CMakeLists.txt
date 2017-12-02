# Find Numpy include paths.

find_package(FFTW3 REQUIRED)

file(GLOB PYFFTW_SRC "*.pyx" )
cython_add_module( pyfftw ${PYFFTW_SRC} )

target_link_libraries( pyfftw ${FFTW_LIBRARIES} )
