add_executable(scene2pset scene2pset.cc)
target_link_libraries(scene2pset PUBLIC mve::core OpenMP::OpenMP_CXX)

install(TARGETS scene2pset RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}/mve/)