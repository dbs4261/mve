add_executable(dmrecon dmrecon.cc fancy_progress_printer.cc)
target_include_directories(dmrecon
  PUBLIC
    ${PNG_INCLUDE_DIR}
    ${TIFF_INCLUDE_DIR}
    ${JPEG_INCLUDE_DIR}
    ${CMAKE_HOME_DIRECTORY}/libs/
)
target_link_libraries(dmrecon
  PUBLIC
    ${PNG_LIBRARY}
    ${TIFF_LIBRARY}
    ${JPEG_LIBRARY}
    Threads::Threads
    mve_util
    mve
    mve_dmrecon
)