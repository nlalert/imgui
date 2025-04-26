cmake_minimum_required(VERSION 3.16)
project(ImGui)

# Set C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Define output directories
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

# ImGui source files
set(IMGUI_SOURCES
    imgui.cpp
    imgui_draw.cpp
    imgui_tables.cpp
    imgui_widgets.cpp
    imgui_demo.cpp
)

# ImGui header files
set(IMGUI_HEADERS
    imconfig.h
    imgui.h
    imgui_internal.h
    imstb_rectpack.h
    imstb_textedit.h
    imstb_truetype.h
)

# Create static library
add_library(ImGui STATIC ${IMGUI_SOURCES} ${IMGUI_HEADERS})

# Set include directories
target_include_directories(ImGui PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

# Platform-specific configurations
if(WIN32)
    # Windows-specific settings
    set(CMAKE_MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
elseif(UNIX AND NOT APPLE)
    # Linux-specific settings
    set(CMAKE_POSITION_INDEPENDENT_CODE ON)
endif()

# Configuration-specific settings
target_compile_options(ImGui PRIVATE
    $<$<CONFIG:Debug>:-g>
    $<$<CONFIG:Release>:-O3>
    $<$<CONFIG:Dist>:-O3>
)

# Export symbols option - This is equivalent to staticruntime "off"
set_target_properties(ImGui PROPERTIES
    POSITION_INDEPENDENT_CODE ON
)
