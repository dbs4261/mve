add_executable(test_util
    gtest_aligned_memory.cc
    gtest_endian.cc
    gtest_file_system.cc
    gtest_string.cc
    gtest_tokenizer.cc
)
target_link_libraries(test_util mve::util GTest::GTest GTest::Main)
add_test(AllTestsIn test_util)