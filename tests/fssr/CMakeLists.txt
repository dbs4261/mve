add_executable(test_fssr
    gtest_iso_octree.cc
    gtest_mesh_clean.cc
    gtest_octree.cc
    gtest_octree_iterator.cc
)
target_link_libraries(test_fssr mve::fssr GTest::GTest GTest::Main)
add_test(AllTestsIn test_fssr)