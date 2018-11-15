cmake_minimum_required(VERSION 2.8.3)
project(cantcoap)

## Use c++ 11x std
set(CMAKE_CXX_FLAGS "-std=c++11  ${CMAKE_CXX_FLAGS}")
if (${CMAKE_EXTRA_GENERATOR} MATCHES "Eclipse CDT4")
    set(CMAKE_CXX_COMPILER_ARG1 "-std=c++11" CACHE STRING "C++ version for eclipse" FORCE)
    set(CMAKE_ECLIPSE_VERSION "4.5" CACHE STRING "Eclipse version" FORCE)
    add_definitions (-DCMAKE_ECLIPSE_GENERATE_SOURCE_PROJECT=TRUE)
endif (${CMAKE_EXTRA_GENERATOR} MATCHES "Eclipse CDT4")

## Enable backtraces
set(CMAKE_CXX_FLAGS "-rdynamic ${CMAKE_CXX_FLAGS}")

find_package(catkin QUIET)
if (catkin_FOUND)
    find_package(catkin REQUIRED COMPONENTS )
else (catkin_FOUND)
    set(catkin_LIBRARIES )
endif(catkin_FOUND)

set(cantcoap_INCLUDE_DIRECTORIES
    include
)       


include_directories(${cantcoap_INCLUDE_DIRECTORIES} ${catkin_INCLUDE_DIRS})

if(catkin_FOUND)
    catkin_package(
    INCLUDE_DIRS include
    LIBRARIES cantcoap
    CATKIN_DEPENDS
)
endif(catkin_FOUND)

add_library(cantcoap
        src/cantcoap.cpp
	src/nethelper.c
)


