cmake_minimum_required(VERSION 2.8)

PROJECT(mpu9250_sample)

## Default install prefix : /usr
SET(CMAKE_INSTALL_PREFIX /usr)
option(CMAKE_INSTALL_PREFIX "CMAKE_INSTALL_PREFIX" ${CMAKE_INSTALL_PREFIX})

## Default build type : REALEASE
IF (CMAKE_BUILD_TYPE STREQUAL "")
	SET(CMAKE_BUILD_TYPE RELEASE)
ENDIF (CMAKE_BUILD_TYPE STREQUAL "")

option(BUILD_HOST "BUILD TARGET [ HOST / TARGET ]" OFF)
IF( ${BUILD_HOST} STREQUAL "ON" )
  add_definitions(-DBUILD_HOST)
ENDIF( ${BUILD_HOST} STREQUAL "ON" )

INCLUDE_DIRECTORIES( ${CMAKE_BINARY_DIR} )

SET(EXECUTABLE_OUTPUT_PATH "${mpu9250_sample_BINARY_DIR}/bin")
SET(LIBRARY_OUTPUT_PATH "${mpu9250_sample_BINARY_DIR}/lib")

INCLUDE_DIRECTORIES( include )
ADD_SUBDIRECTORY( thirdparty )
ADD_SUBDIRECTORY( src )

INSTALL(FILES data/mpu9250.sh DESTINATION /etc/init.d/)
INSTALL(FILES data/RTIMULib.ini DESTINATION share/mpu9250/)
INSTALL(FILES bin/low-speed-spidev.ko DESTINATION bin)
