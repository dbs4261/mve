add_executable(mesh2pset mesh2pset.cc)
target_include_directories(mesh2pset
  PUBLIC
    ${PNG_INCLUDE_DIR}
    ${TIFF_INCLUDE_DIR}
    ${JPEG_INCLUDE_DIR}
    ${CMAKE_HOME_DIRECTORY}/libs/
)
target_link_libraries(mesh2pset
  PUBLIC
    ${PNG_LIBRARY}
    ${TIFF_LIBRARY}
    ${JPEG_LIBRARY}
    mve_util
    mve
    mve_fssr
)