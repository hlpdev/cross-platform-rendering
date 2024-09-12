cmake_minimum_required(VERSION 3.29)
project(rendering_test)

add_definitions(-Wno-deprecated-declarations)

find_package(OpenGL REQUIRED)
find_package(glfw3 3.3 REQUIRED)
find_package(spdlog REQUIRED)
find_package(GLUT REQUIRED)

set(IMGUI_SRC
        imgui/imgui.cpp
        imgui/imgui_draw.cpp
        imgui/imgui_widgets.cpp
        imgui/imgui_tables.cpp
        imgui/backends/imgui_impl_glfw.cpp
        imgui/backends/imgui_impl_opengl3.cpp
        imgui/backends/imgui_impl_glut.cpp
)

set(INCLUDE_DIRS ${OPENGL_INCLUDE_DIR} ${GLUT_INCLUDE_DIR} imgui imgui/backends)
set(LIBRARIES ${OPENGL_LIBRARIES} ${GLUT_LIBRARIES} glfw spdlog::spdlog)

if (APPLE)
    set(CMAKE_CXX_FLAGS "-framework Cocoa -framework IOKit")
    add_compile_definitions(GL_SILENCE_DEPRECATION)
endif()

include_directories(${INCLUDE_DIRS})

file(GLOB SOURCE_FILES ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)
file(GLOB INCLUDE_FILES ${CMAKE_CURRENT_SOURCE_DIR}/*.h)

set(CMAKE_CXX_STANDARD 26)

add_executable(rendering_test ${SOURCE_FILES} ${INCLUDE_FILES} ${IMGUI_SRC})
target_link_libraries(rendering_test ${LIBRARIES})