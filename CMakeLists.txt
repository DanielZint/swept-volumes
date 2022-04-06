cmake_minimum_required(VERSION 3.11)
project(swept-volumes LANGUAGES CXX)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

# libigl
find_package(libigl CONFIG REQUIRED)
find_package(imguizmo CONFIG REQUIRED)

# Add the files containing your project's core functionality (but not exectuable
# main() functions)
file(GLOB SRCFILES include/*.cpp)
add_library(core ${SRCFILES})
target_include_directories(core PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include/)
# these files may depend on libigl
target_link_libraries(core igl::core igl::opengl)

# 
add_executable(swept-volumes-gui swept-volumes-gui.cpp)
target_link_libraries(swept-volumes-gui core igl::core igl::opengl_glfw igl::opengl_glfw_imgui)

target_compile_definitions(swept-volumes-gui PRIVATE SOURCE_DIR="${CMAKE_SOURCE_DIR}")


