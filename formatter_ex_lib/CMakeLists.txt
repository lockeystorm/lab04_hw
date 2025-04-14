cmake_minimum_required(VERSION 3.30)
project(formatter_ex)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(../formatter_lib formatter)

add_library(formatter_ex STATIC formatter_ex.cpp formatter_ex.h)

target_include_directories(formatter_ex PUBLIC ../formatter_lib ${CMAKE_CURRENT_SOURCE_DIR})

target_link_libraries(formatter_ex PUBLIC formatter)
