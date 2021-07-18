add_executable(meshclean meshclean.cc)
target_link_libraries(meshclean PUBLIC mve::fssr)

install(TARGETS meshclean RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}/mve/)