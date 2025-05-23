cmake_minimum_required(VERSION 3.30)
project(equation)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_subdirectory(../formatter_ex_lib formatter_ex)
add_subdirectory(../solver_lib solver)

add_executable(equation equation.cpp)

target_link_libraries(equation formatter_ex solver)
