cmake_minimum_required(VERSION 3.18)

project(WebUI)

include(FetchContent)

option(BUILD_SHARED_LIBS "Build using shared libraries" OFF)
option(WEBUI_BUILD_SHARED_LIBS "Build WebUI using shared libraries" OFF)

FetchContent_Declare(
    civetweb
    GIT_REPOSITORY https://github.com/DeepForge-Technology/civetweb.git
)
FetchContent_MakeAvailable(civetweb)
include_directories(${civetweb_SOURCE_DIR}/include)
message(${civetweb_SOURCE_DIR}/include)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
# Source files
set(SOURCES
    ./src/webui.c
)

set(LIBRARIES civetweb)
# Build the library
if (BUILD_SHARED_LIBS OR WEBUI_BUILD_SHARED_LIBS)
add_library(webui-shared SHARED ${SOURCES})
target_link_libraries(webui-shared ${LIBRARIES})
else()
add_library(webui-static STATIC ${SOURCES})
target_link_libraries(webui-static ${LIBRARIES})
endif()