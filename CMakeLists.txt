cmake_minimum_required(VERSION 3.18)

project(WebUI)

include(FetchContent)

FetchContent_Declare(
    civetweb
    GIT_REPOSITORY https://github.com/DeepForge-Technology/civetweb.git
)
FetchContent_MakeAvailable(civetweb)
link_directories(${civetweb_BINARY_DIR}/Debug/)
include_directories(${civetweb_SOURCE_DIR}/include)
include_directories(${CMAKE_SOURCE_DIR}/include)
# Source files
set(SOURCES
    ./include/webui.hpp
    ./include/webui.h
    ./src/webui.c
)


set(LIBRARIES civetweb)
# Build the library
add_library(webui-static STATIC ${SOURCES})
target_link_libraries(webui-static ${LIBRARIES})
