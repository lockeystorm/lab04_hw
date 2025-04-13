cmake_minimum_required(VERSION 3.30)
project(formatter)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(LIB_SOURCE formatter.h formatter.cpp)

add_library(formatter STATIC ${LIB_SOURCE})

target_include_directories(formatter PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")
