set(MVE_DMRECON_SOURCE
    dmrecon.cc
    global_view_selection.cc
    image_pyramid.cc
    local_view_selection.cc
    mvs_tools.cc
    patch_optimization.cc
    patch_sampler.cc
    single_view.cc
)
set(MVE_DMRECON_PRIVATE_HEADER "")
set(MVE_DMRECON_PUBLIC_HEADER
    defines.h
    dmrecon.h
    global_view_selection.h
    image_pyramid.h
    local_view_selection.h
    mvs_tools.h
    patch_optimization.h
    patch_sampler.h
    progress.h
    settings.h
    single_view.h
    view_selection.h
)

add_library(mve_dmrecon ${MVE_DMRECON_SOURCE})
set_target_properties(mve_dmrecon PROPERTIES
    PUBLIC_HEADER "${MVE_DMRECON_PUBLIC_HEADER}"
    PRIVATE_HEADER "${MVE_DMRECON_PRIVATE_HEADER}"
)

add_library(mve::dmrecon ALIAS mve_dmrecon)

target_include_directories(mve_dmrecon PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/mve/dmrecon/>
)
target_link_libraries(mve_dmrecon PUBLIC mve_settings mve::core Threads::Threads)

install(TARGETS mve_dmrecon EXPORT mve-targets
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/mve/dmrecon/
    PRIVATE_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/mve/private/dmrecon/
)