#find_package(fftw3 REQUIRED)

set(FIND_LIBRARY_USE_LIB64_PATHS ON)

find_path( FFTW3_INCLUDE_DIR fftw3.h )
message(STATUS "FFTW3_INCLUDE_DIR ${FFTW3_INCLUDE_DIR}")
include_directories( ${FFTW3_INCLUDE_DIR} )

find_library( FFTW3_LIBRARY fftw3 PATHS /usr/lib /usr/local/lib /opt/lib )
message(STATUS "FFTW3_LIBRARY ${FFTW3_LIBRARY}")
find_library( FFTW3_THREAD_LIBRARY NAMES fftw3_threads
    PATHS /usr/lib /usr/local/lib /opt/lib
    )

# HACK: FFTW3 library.
set(STATIC_FFTW3 OFF)
if(NOT FFTW3_THREAD_LIBRARY)
    message(STATUS "HACK: Using another method to locate thread" )
    find_file( FFTW3_THREAD_LIBRARY NAMES 
        libfftw3_threads.so libfftw3_threads.so.3 
        PATHS /usr /opt
        PATH_SUFFIXES lib lib64 
        )
    set(STATIC_FFTW3 ON)
endif( )
message(STATUS "FFTW3_THREAD_LIBRARY ${FFTW3_THREAD_LIBRARY}")

set(FFTW3_LIBRARIES ${FFTW3_LIBRARY} ${FFTW3_THREAD_LIBRARY})

file(GLOB PYFFTW_SRC "*.pyx" )
cython_add_module( pyfftw ${PYFFTW_SRC} )

target_link_libraries( pyfftw ${FFTW3_LIBRARY} )
if(NOT STATIC_FFTW3)
    target_link_libraries( pyfftw ${FFTW3_THREAD_LIBRARY} )
else( )
    target_link_libraries( pyfftw  ${FFTW3_THREAD_LIBRARY} )
endif( )

