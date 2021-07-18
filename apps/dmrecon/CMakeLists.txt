add_executable(dmrecon dmrecon.cc fancy_progress_printer.h fancy_progress_printer.cc)
target_link_libraries(dmrecon PUBLIC mve::dmrecon OpenMP::OpenMP_CXX)

install(TARGETS dmrecon RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}/mve/)