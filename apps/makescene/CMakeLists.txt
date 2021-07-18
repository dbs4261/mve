add_executable(makescene makescene.cc)
target_link_libraries(makescene PUBLIC mve::core OpenMP::OpenMP_CXX)

install(TARGETS makescene RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}/mve/)