set(MVE_CORE_SOURCE
    bundle.cc
    bundle_io.cc
    camera.cc
    depthmap.cc
    image_exif.cc
    image_io.cc
    image_tools.cc
    marching.cc
    mesh.cc
    mesh_info.cc
    mesh_io.cc
    mesh_io_npts.cc
    mesh_io_obj.cc
    mesh_io_off.cc
    mesh_io_pbrt.cc
    mesh_io_ply.cc
    mesh_io_smf.cc
    mesh_tools.cc
    scene.cc
    view.cc
    volume.cc
)
set(MVE_CORE_PRIVATE_HEADER "")
set(MVE_CORE_PUBLIC_HEADER
    bundle.h
    bundle_io.h
    camera.h
    defines.h
    depthmap.h
    image.h
    image_base.h
    image_color.h
    image_drawing.h
    image_exif.h
    image_io.h
    image_tools.h
    marching_cubes.h
    marching_tets.h
    mesh.h
    mesh_info.h
    mesh_io.h
    mesh_io_npts.h
    mesh_io_obj.h
    mesh_io_off.h
    mesh_io_pbrt.h
    mesh_io_ply.h
    mesh_io_smf.h
    mesh_tools.h
    scene.h
    view.h
    volume.h
)

add_library(mve_core ${MVE_CORE_SOURCE})
set_target_properties(mve_core PROPERTIES
    PUBLIC_HEADER "${MVE_CORE_PUBLIC_HEADER}"
    PRIVATE_HEADER "${MVE_CORE_PRIVATE_HEADER}"
)

add_library(mve::core ALIAS mve_core)

target_include_directories(mve_core PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/mve/core/>
)
target_link_libraries(mve_core PUBLIC mve_settings mve::util mve::math Threads::Threads TIFF::TIFF PNG::PNG JPEG::JPEG)

install(TARGETS mve_core EXPORT mve-targets
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/mve/core/
    PRIVATE_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/mve/private/core/
)