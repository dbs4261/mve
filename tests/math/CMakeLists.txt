add_executable(test_math
    gtest_accum.cc
    gtest_algo.cc
    gtest_defines.cc
    gtest_functions.cc
    gtest_geom.cc
    gtest_matrix.cc
    gtest_matrix_qr.cc
    gtest_matrix_svd.cc
    gtest_matrix_tools.cc
    gtest_quaternion.cc
    gtest_vector.cc
)
target_link_libraries(test_math mve::math GTest::GTest GTest::Main)
add_test(AllTestsIn test_math)