cmake_minimum_required(VERSION 3.16)
project(ImGui)

# ImGui source files
set(SOURCES
    imgui.cpp
    imgui_draw.cpp
    imgui_tables.cpp
    imgui_widgets.cpp
    imgui_demo.cpp
)

# ImGui header files
set(HEADERS
    imconfig.h
    imgui.h
    imgui_internal.h
    imstb_rectpack.h
    imstb_textedit.h
    imstb_truetype.h
)

# Create static library
add_library(ImGui STATIC ${SOURCES} ${HEADERS})

# Set include directories
target_include_directories(ImGui PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

# Set compiler options
if(MSVC)
    target_compile_options(ImGui PRIVATE /W4)
else()
    target_compile_options(ImGui PRIVATE -Wall -Wextra -Wpedantic)
endif()
