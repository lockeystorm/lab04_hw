cmake_minimum_required(VERSION 3.30)
project(equation)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(equation equation.cpp)

target_link_libraries(equation formatter_ex solver)
