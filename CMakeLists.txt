cmake_minimum_required(VERSION 3.6.0)

include_directories(
        ${CMAKE_SOURCE_DIR}/src/main/cpp/include
)

add_library(libopencv_java4 SHARED IMPORTED)
set_target_properties(
        libopencv_java4
        PROPERTIES IMPORTED_LOCATION
        ${CMAKE_SOURCE_DIR}/src/main/jniLibs/libs/${ANDROID_ABI}/libopencv_java4.so)

add_library(libc++_shared SHARED IMPORTED)
set_target_properties(
        libc++_shared
        PROPERTIES IMPORTED_LOCATION
        ${CMAKE_SOURCE_DIR}/src/main/jniLibs/libs/${ANDROID_ABI}/libc++_shared.so)


add_library(
        Dummy
        SHARED
        src/main/cpp/dummy.cpp
)


find_library(
        log-lib
        log
)

target_link_libraries(
        Dummy libopencv_java4 libc++_shared
        ${log-lib}
)