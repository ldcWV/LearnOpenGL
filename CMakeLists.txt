cmake_minimum_required(VERSION 3.10)
project(learnopengl)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

set(LIB_SOURCES
    lib/Camera.cpp
    lib/Shader.cpp
)

find_package( OpenGL REQUIRED )
add_subdirectory( external/glfw )
add_subdirectory( external/glad )

set(EXECUTABLES
    getting-started
)

foreach(EXECUTABLE ${EXECUTABLES})
    set(SOURCE_FILE "src/${EXECUTABLE}/main.cpp")
    add_executable(${EXECUTABLE} ${SOURCE_FILE} ${LIB_SOURCES})
    target_link_libraries( ${EXECUTABLE} ${OPENGL_LIBRARIES} glfw glad )
    target_include_directories(${EXECUTABLE}
        PRIVATE
            ${OPENGL_INCLUDE_DIRS}
            ${PROJECT_SOURCE_DIR}/external
            ${PROJECT_SOURCE_DIR}/lib
    )
    target_compile_definitions(${EXECUTABLE} PUBLIC SRC_DIR="${CMAKE_CURRENT_SOURCE_DIR}/src/${EXECUTABLE}/")
endforeach(EXECUTABLE ${EXECUTABLES})
