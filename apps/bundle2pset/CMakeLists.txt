add_executable(bundle2pset bundle2pset.cc)
target_include_directories(bundle2pset
  PUBLIC
    ${PNG_INCLUDE_DIR}
    ${TIFF_INCLUDE_DIR}
    ${JPEG_INCLUDE_DIR}
    ${CMAKE_HOME_DIRECTORY}/libs/
)
target_link_libraries(bundle2pset
  PUBLIC
    ${PNG_LIBRARY}
    ${TIFF_LIBRARY}
    ${JPEG_LIBRARY}
    mve_util
    mve
)