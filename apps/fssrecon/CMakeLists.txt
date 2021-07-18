add_executable(fssrecon fssrecon.cc)
target_link_libraries(fssrecon PUBLIC mve::fssr)

install(TARGETS fssrecon RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}/mve/)