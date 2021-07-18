add_executable(test_sfm
    gtest_ba_cholesky.cc
    gtest_ba_conjugate_gradient.cc
    gtest_ba_dense_vector.cc
    gtest_ba_sparse_matrix.cc
    gtest_bundler_tracks.cc
    gtest_homography.cc
    gtest_matching.cc
    gtest_nearest_neighbor.cc
    gtest_pose.cc
    gtest_pose_p3p.cc
    gtest_surf.cc
)
target_link_libraries(test_sfm mve::sfm GTest::GTest GTest::Main)
add_test(AllTestsIn test_sfm)