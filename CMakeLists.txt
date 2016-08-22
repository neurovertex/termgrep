cmake_minimum_required(VERSION 3.5)
include(ExternalProject)
project(termgrep VERSION 0.1 LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED true)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -pedantic")

add_subdirectory(./deps/gvpp)

include_directories(${gvpp_SOURCE_DIR}/src ./deps/json/src)
#link_directories("./lib")
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY "./lib")
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY "./lib")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "./bin")

add_library(termgrep src/termgrep.hpp src/termgrep.cpp)
add_executable(termgrep_main src/main.cpp)
add_executable(termgrep_test src/test.cpp)
target_compile_definitions(termgrep PRIVATE CTYPE=char)
target_compile_definitions(termgrep_main PRIVATE CTYPE=char)
target_compile_definitions(termgrep_test PRIVATE CTYPE=char)

add_library(wtermgrep src/termgrep.hpp src/termgrep.cpp)
add_executable(wtermgrep_main src/main.cpp)
add_executable(wtermgrep_test src/test.cpp)
target_compile_definitions(wtermgrep PRIVATE CTYPE=wchar_t)
target_compile_definitions(wtermgrep_main PRIVATE CTYPE=wchar_t)
target_compile_definitions(wtermgrep_test PRIVATE CTYPE=wchar_t)

target_link_libraries(termgrep_main termgrep gvpp)
target_link_libraries(wtermgrep_main wtermgrep gvpp)
target_link_libraries(termgrep_test termgrep gvpp)
target_link_libraries(wtermgrep_test wtermgrep gvpp)