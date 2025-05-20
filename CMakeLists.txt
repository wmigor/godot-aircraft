cmake_minimum_required(VERSION 3.10)

project(Aircraft)

SET(CMAKE_CXX_FLAGS "-std=c++17")

include(FetchContent)
FetchContent_Declare(
  godot
  GIT_REPOSITORY https://github.com/godotengine/godot-cpp.git
  GIT_TAG 4.4
)
FetchContent_MakeAvailable(godot)

file(GLOB_RECURSE SOURCES CONFIGURE_DEPENDS "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp")
add_compile_definitions(GLM_ENABLE_EXPERIMENTAL)
add_library(${PROJECT_NAME} SHARED ${SOURCES})
target_link_libraries(${PROJECT_NAME} PUBLIC godot::cpp)
