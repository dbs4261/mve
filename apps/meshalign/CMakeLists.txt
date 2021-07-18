add_executable(meshalign meshalign.cc
    meshlab_alignment.h
    meshlab_alignment.cc
    range_image.h
    stanford_alignment.h
    stanford_alignment.cc
)
target_link_libraries(meshalign PUBLIC mve::core)

install(TARGETS meshalign RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}/mve/)