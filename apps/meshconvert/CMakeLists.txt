add_executable(meshconvert meshconvert.cc)
target_link_libraries(meshconvert PUBLIC mve::core)

install(TARGETS meshconvert RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}/mve/)