cmake_minimum_required (VERSION 2.6)

project( FaceOff )
set (FaceOff_VERSION_MAJOR 1)
set (FaceOff_VERSION_MINOR 0)

# We need OpenCV 
find_package(OpenCV)

# And OpenNI
set(OPENNI_INCLUDE_DIR "/usr/include/openni2")
include_directories( "${OPENNI_INCLUDE_DIR}" )

set(OPENNI_LIB_DIR "/usr/lib")
link_directories( "${OPENNI_LIB_DIR}" )
find_library( OPENNI2 libOpenNI2.so )

#set ( PROJECT_LINK_LIBS libOpenNI2.so )

# Add the binary tree to the search path for inlcude files
include_directories( "src")
include_directories( "${PROJECT_BINARY_DIR}" )

# configure a header file to pass some of the CMake settings
# to the source code
configure_file (
  "src/FaceOffConfig.h.in"
  "FaceOffConfig.h"
  )

# Add the binary tree to the search path for inlcude files
file(GLOB SOURCES "src/*.cpp")

add_executable(FaceOff ${SOURCES})

# Link with OpnNI libs
target_link_libraries( FaceOff "${OPENNI2}" )