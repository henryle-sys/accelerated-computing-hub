cmake_minimum_required(VERSION 3.20)
project(HenryPractice CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CUDA_STANDARD 17)

file(GLOB SOURCES "*.cu" "*.cpp" "*.c")
file(GLOB HEADERS "*.h" "*.hpp" "*.cuh")

add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS})

target_include_directories(${PROJECT_NAME} PRIVATE
        ${CMAKE_CUDA_TOOLKIT_INCLUDE_DIRECTORIES}
)