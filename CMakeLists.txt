cmake_minimum_required(VERSION 3.14)
project(mve LANGUAGES CXX)
set(ignoreMe "${CMAKE_C_COMPILER}")

set(MVE_VERSION 21.3.9)

# Set a default build type if none was specified
if(NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
    message(STATUS "Setting build type to 'RelWithDebInfo' as none was specified.")
    set(CMAKE_BUILD_TYPE RelWithDebInfo CACHE STRING "Choose the type of build." FORCE)
    # Set the possible values of build type for cmake-gui, ccmake
    set_property(CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release" "RelWithDebInfo")
endif()

# Generate compile_commands.json to make it easier to work with clang based tools
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

set(THREADS_PREFER_PTHREAD_FLAG ON)
find_package(Threads REQUIRED)
find_package(OpenMP)

option(BUILD_SHARED_LIBS "This will cause all libraries to be built shared" ON)
option(BUILD_APPS "If the MVE applications should be built" ON)
option(BUILD_TESTS "If the tests should be built" ON)
option(BUILD_DOCS "If the documentation should be built" ON)
option(WITH_GUI "Enable the GUI for MVE that requires OpenGL and GLEW" ON)
option(ENABLE_IPO "Enable Interprocedural Optimization, aka Link Time Optimization (LTO)" ON)
option(ENABLE_PIC "Enable Position Independent Code" ON)
option(ENABLE_DOXYGEN "Enable doxygen doc builds of source" OFF)

add_library(mve_settings INTERFACE)
add_library(mve::settings ALIAS mve_settings)
target_compile_features(mve_settings INTERFACE cxx_std_11)
target_compile_options(mve_settings INTERFACE
    $<$<CXX_COMPILER_ID:GNU>:-Wall -Wextra -Wundef -pedantic>
    $<$<CXX_COMPILER_ID:Clang>:-Weverything -pedantic>
    $<$<CXX_COMPILER_ID:MSVC>:/W3 -DNOMINMAX -D_USE_MATH_DEFINES -D_CRT_SECURE_NO_WARNINGS>
    $<$<AND:$<NOT:$<CONFIG:DEBUG>>,$<CXX_COMPILER_ID:GNU>>:-march=native>
    $<$<AND:$<NOT:$<CONFIG:DEBUG>>,$<CXX_COMPILER_ID:GNU>>:-funsafe-math-optimizations>
    $<$<AND:$<NOT:$<CONFIG:DEBUG>>,$<CXX_COMPILER_ID:GNU>>:-fno-math-errno>
)

install(TARGETS mve_settings EXPORT mve-targets)

include(CheckPIESupported)
check_pie_supported(LANGUAGES CXX)
set_property(TARGET mve_settings PROPERTY POSITION_INDEPENDENT_CODE ${CMAKE_CXX_LINK_PIE_SUPPORTED})

include(CheckIPOSupported)
check_ipo_supported(RESULT CMAKE_CXX_LTO_SUPPORTED LANGUAGES CXX)
set_property(TARGET mve_settings PROPERTY INTERPROCEDURAL_OPTIMIZATION ${CMAKE_CXX_LTO_SUPPORTED})

if(ENABLE_DOXYGEN)
    set(DOXYGEN_CALLER_GRAPH YES)
    set(DOXYGEN_CALL_GRAPH YES)
    set(DOXYGEN_EXTRACT_ALL YES)
    find_package(Doxygen REQUIRED dot)
    doxygen_add_docs(doxygen-docs ${PROJECT_SOURCE_DIR})
endif()

if(CMAKE_CXX_COMPILER_ID MATCHES ".*Clang")
    add_compile_options(-fcolor-diagnostics)
elseif(CMAKE_CXX_COMPILER_ID STREQUAL "GNU")
    add_compile_options(-fdiagnostics-color=always)
endif()

find_package(PNG REQUIRED)
find_package(TIFF REQUIRED)
find_package(JPEG REQUIRED)

find_package(OpenGL QUIET)
find_package(GLEW QUIET)

include(GNUInstallDirs)

add_subdirectory(cmake)

add_subdirectory(libs)

if (BUILD_APPS)
    add_subdirectory(apps)
endif()

if (BUILD_TESTS)
    find_package(GTest REQUIRED)
    add_subdirectory(tests)
endif()

if (BUILD_DOCS)
    find_package(Doxygen REQUIRED dot)
    add_subdirectory(docs)
endif()

install(EXPORT mve-targets
    FILE mve-targets.cmake
    NAMESPACE mve::
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/mve/
)