file (GLOB UMVE_SOURCES "${CMAKE_CURRENT_LIST_DIR}/*.cc")
file (GLOB UMVE_HEADERS "${CMAKE_CURRENT_LIST_DIR}/*.h")
file (GLOB SCENE_ADDINS_SOURCES "${CMAKE_CURRENT_LIST_DIR}/scene_addins/*.cc")
file (GLOB SCENE_ADDINS_HEADERS "${CMAKE_CURRENT_LIST_DIR}/scene_addins/*.h")
file (GLOB SCENE_INSPECT_SOURCES "${CMAKE_CURRENT_LIST_DIR}/scene_inspect/*.cc")
file (GLOB SCENE_INSPECT_HEADERS "${CMAKE_CURRENT_LIST_DIR}/scene_inspect/*.h")
file (GLOB VIEWINSPECT_SOURCES "${CMAKE_CURRENT_LIST_DIR}/viewinspect/*.cc")
file (GLOB VIEWINSPECT_HEADERS "${CMAKE_CURRENT_LIST_DIR}/viewinspect/*.h")

add_executable(umve
    ${UMVE_SOURCES}
    ${UMVE_HEADERS}
    ${SCENE_ADDINS_SOURCES}
    ${SCENE_ADDINS_HEADERS}
    ${SCENE_INSPECT_SOURCES}
    ${SCENE_INSPECT_HEADERS}
    ${VIEWINSPECT_SOURCES}
    ${VIEWINSPECT_HEADERS}
    ${CMAKE_CURRENT_LIST_DIR}/umve.qrc
)

find_package(Qt5 REQUIRED Core Gui OpenGL Svg Widgets)
set_target_properties(umve PROPERTIES AUTOMOC ON AUTORCC ON AUTOUIC ON ENABLE_EXPORTS TRUE)

target_link_libraries(umve PUBLIC Qt5::Gui Qt5::OpenGL Qt5::Svg Qt5::Widgets mve::dmrecon mve::fssr mve::ogl mve::sfm)
target_include_directories(umve PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}>
)
target_compile_options(umve PRIVATE
    $<$<CXX_COMPILER_ID:GNU>:-Wno-deprecated-declarations>
)

file(GLOB SHADERS "${CMAKE_CURRENT_LIST_DIR}/shaders/*")
foreach(SHADER_PATH ${SHADERS})
    file(RELATIVE_PATH SHADER ${CMAKE_CURRENT_LIST_DIR} ${SHADER_PATH})
    configure_file("${CMAKE_CURRENT_LIST_DIR}/${SHADER}" "${CMAKE_CURRENT_BINARY_DIR}/${SHADER}" COPYONLY)
endforeach()

install(TARGETS umve RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR}/mve/)
install(DIRECTORY shaders/ DESTINATION ${CMAKE_INSTALL_DATADIR}/umve/shaders/)