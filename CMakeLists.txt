cmake_minimum_required (VERSION 3.1)

project("approximation_on_voronoi")

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)

add_definitions(-D_CRT_SECURE_NO_WARNINGS)

### NANOGUI
# Disable building extras we won't need (pure C++ project)
set(NANOGUI_BUILD_EXAMPLE OFF CACHE BOOL " " FORCE)
set(NANOGUI_BUILD_PYTHON  OFF CACHE BOOL " " FORCE)
set(NANOGUI_INSTALL       OFF CACHE BOOL " " FORCE)
# you could add the NANOGUI_BUILD_SHARED part here
# Add the configurations from nanogui
add_subdirectory(external/nanogui)  # this executes ext/nanogui/CMakeLists.txt for you
# For reliability of parallel build, make the NanoGUI targets dependencies
set_property(TARGET glfw glfw_objects nanogui PROPERTY FOLDER "nanogui-staff")
# Various preprocessor definitions have been generated by NanoGUI
add_definitions(${NANOGUI_EXTRA_DEFS})
# On top of adding the path to nanogui/include, you may need extras

add_subdirectory(voronoi)

add_subdirectory(renders)

# add_subdirectory(function-version)

add_subdirectory(image-version)

### necessary files
file(COPY external/nanogui/resources DESTINATION ${CMAKE_CURRENT_BINARY_DIR})
