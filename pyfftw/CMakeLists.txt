# Find Numpy include paths.

file(GLOB PYFFTW_SRC "*.pyx" )
cython_add_module( pyfftw ${PYFFTW_SRC} )
