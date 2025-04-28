cmake_minimum_required(VERSION 3.16)
project(ImGui)

# ImGui source files
set(SOURCES
    imgui.cpp
    imgui_draw.cpp
    imgui_tables.cpp
    imgui_widgets.cpp
    imgui_demo.cpp
    # Add the backend implementation files
    backends/imgui_impl_glfw.cpp
    backends/imgui_impl_opengl3.cpp
)

# ImGui header files
set(HEADERS
    imconfig.h
    imgui.h
    imgui_internal.h
    imstb_rectpack.h
    imstb_textedit.h
    imstb_truetype.h
    # Add the backend header files
    backends/imgui_impl_glfw.h
    backends/imgui_impl_opengl3.h
)

# Create static library
add_library(ImGui STATIC ${SOURCES} ${HEADERS})

# Set include directories
target_include_directories(ImGui 
    PUBLIC 
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_CURRENT_SOURCE_DIR}/backends
)

# GLFW is needed for the ImGui GLFW implementation
target_link_libraries(ImGui PUBLIC glfw)

# OpenGL is needed for the ImGui OpenGL implementation
find_package(OpenGL REQUIRED)
target_link_libraries(ImGui PUBLIC ${OPENGL_LIBRARIES})

# Set compiler options
if(MSVC)
    target_compile_options(ImGui PRIVATE /W4)
else()
    target_compile_options(ImGui PRIVATE -Wall -Wextra -Wpedantic)
endif()
