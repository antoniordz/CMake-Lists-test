cmake_minimum_required(VERSION 3.17)

#Set target output directory
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

set(VALID_BUILD_TYPES "Release" "Debug" "MinSizeRel" "RelWithDebInfo")

option(BUILD_SHARED_LIBS "True when building a shared library" True)
project(Foo)

if(NOT MAKE_CONFIGURATION_TYPES)
	if("${CMAKE_BUILD_TYPE}" STREQUAL "")
		set(CMAKE_BUILD_TYPE "Release" CACHE STRING "Build Configuration" FORCE)
	endif()
endif()
#validate the build type
if(NOT MAKE_CONFIGURATION_TYPES)
	list(FIND VALID_BUILD_TYPES "${CMAKE_BUILD_TYPE}" INDEX)
	if(${INDEX} MATCHES -1)
		message(FATAL_ERROR "tipo de construcción invalido. Los validos son [${VALID_BUILD_TYPES}]")
	endif()
endif()

#Create a dropdown list for options
if(NOT MAKE_CONFIGURATION_TYPES)
    if(DEFINED CMAKE_BUILD_TYPE)
        set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS ${VALID_BUILD_TYPES})
    endif()
endif()


add_subdirectory(Foo)

add_subdirectory("examples")
