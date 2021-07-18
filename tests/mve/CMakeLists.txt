add_executable(test_core
    gtest_bundle.cc
    gtest_camera.cc
    gtest_image.cc
    gtest_image_color.cc
    gtest_image_drawing.cc
    gtest_image_io.cc
    gtest_image_tools.cc
    gtest_mesh_info.cc
    gtest_mesh_io.cc
    gtest_mesh_tools.cc
    gtest_scene.cc
    gtest_triangle_mesh.cc
    gtest_view.cc
)
target_link_libraries(test_core mve::core GTest::GTest GTest::Main)
add_test(AllTestsIn test_core)