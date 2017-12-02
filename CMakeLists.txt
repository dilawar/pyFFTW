cmake_minimum_required(VERSION 2.6)
project(PyFFTW)
cmake_policy(SET CMP0011 NEW)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

find_package(PythonInterp REQUIRED)
include( UseCython )

find_package(NumPy REQUIRED)
include_directories( ${PYTHON_NUMPY_INCLUDE_DIR} )

include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/include )
add_subdirectory( ${CMAKE_CURRENT_SOURCE_DIR}/pyfftw )

