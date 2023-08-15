cmake_minimum_required(VERSION 3.15)
project(LibraryNameTests)

set(CMAKE_CXX_STANDARD 20)

add_executable(${PROJECT_NAME})

target_link_libraries(${PROJECT_NAME} PRIVATE libraryname gtest gtest_main)
