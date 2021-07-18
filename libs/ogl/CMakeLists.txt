set(MVE_OGL_SOURCE
    camera_2d.cc
    camera_trackball.cc
    events.cc
    mesh_renderer.cc
    render_tools.cc
    shader_program.cc
    texture.cc
    vertex_array.cc
    vertex_buffer.cc
)
set(MVE_OGL_PRIVATE_HEADER "")
set(MVE_OGL_PUBLIC_HEADER
        camera.h
        camera_2d.h
        camera_trackball.h
        check_gl_error.h
        context.h
        defines.h
        events.h
        key_symbols.h
        mesh_renderer.h
        opengl.h
        render_tools.h
        shader_program.h
        texture.h
        vertex_array.h
        vertex_buffer.h
)

add_library(mve_ogl ${MVE_OGL_SOURCE})
set_target_properties(mve_ogl PROPERTIES
    PUBLIC_HEADER "${MVE_OGL_PUBLIC_HEADER}"
    PRIVATE_HEADER "${MVE_OGL_PRIVATE_HEADER}"
)

add_library(mve::ogl ALIAS mve_ogl)

target_include_directories(mve_ogl PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/../>
    $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}/mve/ogl/>
)
target_link_libraries(mve_ogl PUBLIC mve_settings mve::core GLEW::GLEW OpenGL::GL Threads::Threads)
target_compile_definitions(mve_ogl PUBLIC $<$<BOOL:${OpenGL_GLX_FOUND}>:GL_GLEXT_PROTOTYPES>)

install(TARGETS mve_ogl EXPORT mve-targets
    PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/mve/ogl/
    PRIVATE_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/mve/private/ogl/
)