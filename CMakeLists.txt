cmake_minimum_required(VERSION 2.8)

project(polynomial-systemc CXX)

set(CMAKE_CXX_STANDARD 11) # This is equal to QMAKE_CXX_FLAGS += -std=c++0x
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

set (CMAKE_PREFIX_PATH $ENV{SYSTEMC_HOME})

find_package(SystemCLanguage CONFIG REQUIRED)
set (CMAKE_CXX_STANDARD ${SystemC_CXX_STANDARD})


# poly-eval
include_directories(./src/polynom)
aux_source_directory(./src/polynom POLY-EVAL_SOURCES)
add_library(lib-poly-eval STATIC ${POLY-EVAL_SOURCES})
add_executable(poly-eval ${POLY-EVAL_SOURCES})
target_link_libraries(poly-eval SystemC::systemc)

# poly-int
include_directories(./src)
aux_source_directory(./src POLY-INT_SOURCES)
add_executable(poly-int ${POLY-INT_SOURCES})
target_link_libraries(poly-int lib-poly-eval SystemC::systemc)
