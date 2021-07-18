set(MVE_UTIL_SOURCE
        arguments.cc
        file_system.cc
        ini_parser.cc
        system.cc
)
set(MVE_UTIL_PRIVATE_HEADER "")
set(MVE_UTIL_PUBLIC_HEADER
    aligned_allocator.h
    aligned_memory.h
    arguments.h
    defines.h
    exception.h
    file_system.h
    frame_timer.h
    ini_parser.h
    logging.h
    strings.h
    system.h
    timer.h
    tokenizer.h
)

add_library(mve_util ${MVE_UTIL_SOURCE})
set_target_properties(mve_util PROPERTIES
    PUBLIC_HEADER "${MVE_UTIL_PUBLIC_HEADER}"
    PRIVATE_HEADER "${MVE_UTIL_PRIVATE_HEADER}"
)

add_library(mve::util ALIAS mve_util)

target_include_directories(mve_util PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/mve/util/>
)
target_link_libraries(mve_util PUBLIC mve_settings Threads::Threads)

install(TARGETS mve_util EXPORT mve-targets
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/mve/util/
    PRIVATE_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/mve/private/util/
)