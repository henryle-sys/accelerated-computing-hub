cmake_minimum_required(VERSION 3.20)

set(CMAKE_CUDA_ARCHITECTURES 86)
set(CMAKE_CUDA_COMPILER /usr/local/cuda/bin/nvcc)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CUDA_STANDARD 17)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

project(HenryPractice CUDA CXX)

file(GLOB SOURCES "*.cu" "*.cpp" "*.c")
file(GLOB HEADERS "*.h" "*.hpp" "*.cuh")

add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS})

find_package(CUDAToolkit REQUIRED)

target_link_libraries(${PROJECT_NAME} PRIVATE
        CUDA::cudart
)

target_include_directories(${PROJECT_NAME} PRIVATE
        ${CMAKE_CUDA_TOOLKIT_INCLUDE_DIRECTORIES}
)