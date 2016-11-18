# cmake needs this line
cmake_minimum_required(VERSION 2.8)

# Define project name
project(camcalib)

# Find OpenCV, you may need to set OpenCV_DIR variable
# to the absolute path to the directory containing OpenCVConfig.cmake file
# via the command line or GUI
find_package(OpenCV REQUIRED)

# If the package has been found, several variables will
# be set, you can find the full list with descriptions
# in the OpenCVConfig.cmake file.
# Print some message showing some of them
message(STATUS "OpenCV library status:")
message(STATUS "    version: ${OpenCV_VERSION}")
message(STATUS "    libraries: ${OpenCV_LIBS}")
message(STATUS "    include path: ${OpenCV_INCLUDE_DIRS}")

set(LIB_HEADER_FILES
    CameraIntrinsicsCalibration.h
    )

set(LIB_SOURCE_FILES
    CameraIntrinsicsCalibration.cpp
    )

include_directories(${OpenCV_INCLUDE_DIRS})

# add the library and its dependency
add_library(camcalib
            ${LIB_HEADER_FILES}
            ${LIB_SOURCE_FILES}
            )
target_link_libraries(camcalib
                      ${OpenCV_LIBS}
                      )

# add the test executable and its dependency
add_executable(camcalib_test
               camcalib.cpp
               )
target_link_libraries(camcalib_test
                      camcalib
                      ${OpenCV_LIBS}
                      )

