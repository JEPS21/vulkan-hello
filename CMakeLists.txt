cmake_minimum_required(VERSION 3.23)

project(Hello)

find_package(Vulkan REQUIRED)

set(GLFW_BUILD_DOCS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_TESTS OFF CACHE BOOL "" FORCE)
set(GLFW_BUILD_EXAMPLES OFF CACHE BOOL "" FORCE)

add_subdirectory("external/glfw")

add_executable(hello "src/main.cpp")
set_property(TARGET hello PROPERTY CXX_STANDARD 23)
set_property(TARGET hello PROPERTY CXX_STANDARD_REQUIRED On)

target_link_libraries(hello PRIVATE Vulkan::Vulkan glfw)

if(MSVC)
	target_compile_options(hello PRIVATE /Wall /Za)
else()
	target_compile_options(hello PRIVATE -Wall -Wextra -Wpedantic)
endif()