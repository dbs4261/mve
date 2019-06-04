cmake_minimum_required(VERSION 3.10)
project(SMVS LANGUAGES CXX)

set(ignoreMe "${CMAKE_C_COMPILER}")

find_package(PNG REQUIRED)
find_package(TIFF REQUIRED)
find_package(JPEG REQUIRED)

set(THREADS_PREFER_PTHREAD_FLAG ON)
find_package(Threads)

add_subdirectory(libs)
add_subdirectory(apps)