add_executable(sceneupgrade sceneupgrade.cc)
target_include_directories(sceneupgrade
  PUBLIC
    ${PNG_INCLUDE_DIR}
    ${TIFF_INCLUDE_DIR}
    ${JPEG_INCLUDE_DIR}
    ${CMAKE_HOME_DIRECTORY}/libs/
)
target_link_libraries(sceneupgrade
  PUBLIC
    ${PNG_LIBRARY}
    ${TIFF_LIBRARY}
    ${JPEG_LIBRARY}
    mve_util
    mve
    mve_sfm
)