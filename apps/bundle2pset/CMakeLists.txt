add_executable(bundle2pset bundle2pset.cc)
target_link_libraries(bundle2pset PUBLIC mve_settings mve::core)

install(TARGETS bundle2pset RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}/mve/)