cmake_minimum_required(VERSION 3.30.1)
project(SFML_Template)

set(CMAKE_CXX_STANDARD 23)
set(TESTS_ROOT "${PROJECT_SOURCE_DIR}/tests")
set(SRC_ROOT "${PROJECT_SOURCE_DIR}/src")

file(MAKE_DIRECTORY ${TESTS_ROOT} ${SRC_ROOT} )

include(FetchContent)
set(SFML_BUILD_NETWORK OFF CACHE BOOL "" FORCE)
FetchContent_Declare(
    SFML
    GIT_REPOSITORY "https://github.com/SFML/SFML.git"
    GIT_TAG master
)
FetchContent_MakeAvailable(SFML)

file(GLOB_RECURSE SRC "${SRC_ROOT}/*.cpp")
file(GLOB_RECURSE HEADER "${SRC_ROOT}/*.h")

add_executable(SFML_Template "${TESTS_ROOT}/Source.cpp")

target_link_libraries(SFML_Template
    PRIVATE
        sfml-graphics
        sfml-window
        sfml-system
)
target_sources(SFML_Template   
    PRIVATE
        ${SRC}
    PUBLIC
        FILE_SET HEADERS
        BASE_DIRS src
        FILES ${HEADER}
)

target_include_directories(SFML_Template PUBLIC
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>
    $<INSTALL_INTERFACE:include>
)
