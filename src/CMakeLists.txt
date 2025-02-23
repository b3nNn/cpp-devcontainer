cmake_minimum_required(VERSION 3.23)
project(app VERSION 0.1)

set(CMAKE_CXX_STANDARD 23)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -O0 -ggdb3 -Wall -Wextra -pedantic")

add_executable(${PROJECT_NAME})
target_sources(${PROJECT_NAME} PRIVATE "app.cpp")
target_include_directories(${PROJECT_NAME} PRIVATE "${PROJECT_SOURCE_DIR}")
set_target_properties(${PROJECT_NAME} PROPERTIES 
        VERSION 0.0.1
        SOVERSION 0)
install(TARGETS ${PROJECT_NAME})
