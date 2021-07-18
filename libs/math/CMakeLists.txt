set(MVE_MATH_SOURCE "")
set(MVE_MATH_PRIVATE_HEADER "")
set(MVE_MATH_PUBLIC_HEADER
    accum.h
    algo.h
    bezier_curve.h
    bspline.h
    defines.h
    functions.h
    geometry.h
    line.h
    matrix.h
    matrix_qr.h
    matrix_svd.h
    matrix_tools.h
    octree_tools.h
    permute.h
    plane.h
    quaternion.h
    transform.h
    vector.h
)

add_library(mve_math INTERFACE ${MVE_MATH_SOURCE})
set_target_properties(mve_math PROPERTIES
    PUBLIC_HEADER "${MVE_MATH_PUBLIC_HEADER}"
    PRIVATE_HEADER "${MVE_MATH_PRIVATE_HEADER}"
)

add_library(mve::math ALIAS mve_math)

target_include_directories(mve_math INTERFACE
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/mve/math/>
)
target_link_libraries(mve_math INTERFACE mve_settings Threads::Threads)

install(TARGETS mve_math EXPORT mve-targets
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/mve/math/
    PRIVATE_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/mve/private/math/
)