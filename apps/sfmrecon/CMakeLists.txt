add_executable(sfmrecon sfmrecon.cc)
target_link_libraries(sfmrecon PUBLIC mve::sfm)

install(TARGETS sfmrecon RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}/mve/)