add_executable(sceneupgrade sceneupgrade.cc)
target_link_libraries(sceneupgrade PUBLIC mve::sfm)

install(TARGETS sceneupgrade RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}/mve/)