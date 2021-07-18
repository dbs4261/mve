add_executable(featurerecon featurerecon.cc)
target_link_libraries(featurerecon PUBLIC mve::sfm)

install(TARGETS featurerecon RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}/mve/)