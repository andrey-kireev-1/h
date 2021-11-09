cmake_minimum_required(VERSION 3.12)
set(CMAKE_C_COMPILER "gcc")
set(CMAKE_CC_COMPILER "gcc")

project(hw2)

configure_file(CMakeLists.txt.in
        googletest-download/CMakeLists.txt)
execute_process(COMMAND ${CMAKE_COMMAND} -G "${CMAKE_GENERATOR}" .
        WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/googletest-download )
execute_process(COMMAND ${CMAKE_COMMAND} --build .
        WORKING_DIRECTORY ${CMAKE_BINARY_DIR}/googletest-download )

add_subdirectory(${CMAKE_BINARY_DIR}/googletest-src
        ${CMAKE_BINARY_DIR}/googletest-build)

set(CMAKE_CXX_STANDART 17)
set(CMAKE_CXX_STANDART_REQUIRED ON)
set(CMAKE_CXX_OUTPUT_EXTENSION_REPLACE ON)
set(CMAKE_C_FLAGS " -Wall -Werror -Wpedantic -g3 -ggdb") 
# list(APPEND CMAKE_MODULE_PATH "${CMAKE_SOURCE_DIR}/cmake-modules")
# include(CodeCoverage)
# append_coverage_compiler_flags()

# setup_target_for_coverage_lcov(
#         NAME codeCoverage
#         EXECUTABLE tests
#         BASE_DIRECTORY "${PROJECT_SOURCE_DIR}"
#         EXCLUDE "/usr/*" "${PROJECT_SOURCE_DIR}/project/tests/" "${PROJECT_SOURCE_DIR}/project/src/main.c"
# )

# INCLUDE_DIRECTORIES(project/include)
set(SOURCE_LIB project/src/main.c)	
#add_library(gen include(gtest.cmake)STATIC ${SOURCE_LIB})
add_executable(hw2 project/src/main.c)
target_link_libraries(hw2 gen -lpthread)
find_package(Threads)

#include_directories(${GTEST_INCLUDE_DIRS})
#message(${GTEST_LIBRARIES})
add_executable(tests project/tests/test.cpp)

target_link_libraries(${PROJECT_NAME} gtest ${CMAKE_THREAD_LIBS_INIT})
#target_link_libraries(tests ${GTEST_LIBRARIES} -lpthread)
target_link_libraries(tests gen)

