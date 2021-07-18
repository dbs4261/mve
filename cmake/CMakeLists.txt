include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    mveConfigVersion.cmake
    VERSION ${MVE_VERSION}
    COMPATIBILITY AnyNewerVersion
)

include(CMakePackageConfigHelpers)
configure_package_config_file(
    ${CMAKE_CURRENT_LIST_DIR}/mveConfig.cmake.in
    ${CMAKE_CURRENT_BINARY_DIR}/mveConfig.cmake
    INSTALL_DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/mve/
)

install(FILES
    ${CMAKE_CURRENT_BINARY_DIR}/mveConfig.cmake
    ${CMAKE_CURRENT_BINARY_DIR}/mveConfigVersion.cmake
    DESTINATION ${CMAKE_INSTALL_LIBDIR}/cmake/mve/
)
