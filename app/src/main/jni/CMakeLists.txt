project(ncnnyolox)

cmake_minimum_required(VERSION 3.10)

#set(OpenCV_DIR ${CMAKE_SOURCE_DIR}/opencv/sdk/native/jni)
#find_package(OpenCV REQUIRED core imgproc)

set(ncnn_DIR ${CMAKE_SOURCE_DIR}/ncnn/${ANDROID_ABI}/lib/cmake/ncnn)
find_package(ncnn REQUIRED)

set(xgen_path ${CMAKE_SOURCE_DIR}/../jniLibs/${ANDROID_ABI}/libxgen.so)
add_library (xgen SHARED IMPORTED)
set_target_properties(xgen PROPERTIES IMPORTED_LOCATION "${xgen_path}")
include_directories(${CMAKE_SOURCE_DIR}/xgen/include)

add_library(ncnnyolox SHARED yoloxncnn.cpp yolox.cpp ndkcamera.cpp)

#target_link_libraries(ncnnyolox ncnn ${OpenCV_LIBS} camera2ndk mediandk)
target_link_libraries(ncnnyolox ncnn  camera2ndk mediandk xgen)