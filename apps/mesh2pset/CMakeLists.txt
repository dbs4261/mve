add_executable(mesh2pset mesh2pset.cc)
target_link_libraries(mesh2pset PUBLIC mve::core)

install(TARGETS mesh2pset RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}/mve/)