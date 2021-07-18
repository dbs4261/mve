set(MVE_SFM_SOURCE
        ba_linear_solver.cc
        bundle_adjustment.cc
        bundler_common.cc
        bundler_features.cc
        bundler_incremental.cc
        bundler_init_pair.cc
        bundler_intrinsics.cc
        bundler_matching.cc
        bundler_tracks.cc
        camera_database.cc
        cascade_hashing.cc
        exhaustive_matching.cc
        extract_focal_length.cc
        feature_set.cc
        fundamental.cc
        homography.cc
        matching.cc
        nearest_neighbor.cc
        pose_p3p.cc
        ransac.cc
        ransac_fundamental.cc
        ransac_homography.cc
        ransac_pose_p3p.cc
        sift.cc
        surf.cc
        triangulate.cc
        visualizer.cc
)
set(MVE_SFM_PRIVATE_HEADER "")
set(MVE_SFM_PUBLIC_HEADER
    ba_cholesky.h
    ba_conjugate_gradient.h
    ba_dense_vector.h
    ba_linear_solver.h
    ba_sparse_matrix.h
    ba_types.h
    bundle_adjustment.h
    bundler_common.h
    bundler_features.h
    bundler_incremental.h
    bundler_init_pair.h
    bundler_intrinsics.h
    bundler_matching.h
    bundler_tracks.h
    camera_database.h
    camera_pose.h
    cascade_hashing.h
    correspondence.h
    defines.h
    exhaustive_matching.h
    extract_focal_length.h
    feature_set.h
    fundamental.h
    homography.h
    matching.h
    matching_base.h
    nearest_neighbor.h
    pose_p3p.h
    ransac.h
    ransac_fundamental.h
    ransac_homography.h
    ransac_pose_p3p.h
    sift.h
    surf.h
    triangulate.h
    visualizer.h
)

add_library(mve_sfm ${MVE_SFM_SOURCE})
set_target_properties(mve_sfm PROPERTIES
    PUBLIC_HEADER "${MVE_SFM_PUBLIC_HEADER}"
    PRIVATE_HEADER "${MVE_SFM_PRIVATE_HEADER}"
)

add_library(mve::sfm ALIAS mve_sfm)

target_include_directories(mve_sfm PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/mve/sfm/>
)
target_link_libraries(mve_sfm PUBLIC mve_settings mve::core Threads::Threads $<$<BOOL:${OpenMP_FOUND}>:OpenMP::OpenMP_CXX>)

install(TARGETS mve_sfm EXPORT mve-targets
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/mve/sfm/
    PRIVATE_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/mve/private/sfm/
)