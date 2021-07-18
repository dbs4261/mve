set(MVE_FSSR_SOURCE
    basis_function.cc
    hermite.cc
    iso_octree.cc
    iso_surface.cc
    mesh_clean.cc
    octree.cc
    sample_io.cc
    triangulation.cc
    voxel.cc
)
set(MVE_FSSR_PRIVATE_HEADER "")
set(MVE_FSSR_PUBLIC_HEADER
    basis_function.h
    defines.h
    hermite.h
    iso_octree.h
    iso_surface.h
    mesh_clean.h
    octree.h
    sample.h
    sample_io.h
    triangulation.h
    voxel.h
)

add_library(mve_fssr ${MVE_FSSR_SOURCE})
set_target_properties(mve_fssr PROPERTIES
    PUBLIC_HEADER "${MVE_FSSR_PUBLIC_HEADER}"
    PRIVATE_HEADER "${MVE_FSSR_PRIVATE_HEADER}"
)

add_library(mve::fssr ALIAS mve_fssr)

target_include_directories(mve_fssr PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../>
        $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/mve/fssr/>
)
target_link_libraries(mve_fssr
    PUBLIC
        mve_settings mve::core Threads::Threads
    PRIVATE
        $<$<BOOL:${OpenMP_FOUND}>:OpenMP::OpenMP_CXX>
)

install(TARGETS mve_fssr EXPORT mve-targets
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/mve/fssr/
    PRIVATE_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/mve/private/fssr/
)