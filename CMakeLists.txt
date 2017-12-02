cmake_minimum_required(VERSION 2.6)
project(PyFFTW)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

find_package(PythonInterp REQUIRED)
include( UseCython )

include_directories( ${CMAKE_CURRENT_SOURCE_DIR}/include )
add_subdirectory( ${CMAKE_CURRENT_SOURCE_DIR}/pyfftw )

