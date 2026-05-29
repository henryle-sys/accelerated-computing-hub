cmake_minimum_required(VERSION 3.20)
project(HenryPractice CUDA CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CUDA_STANDARD 17)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)  # ← critical for clangd

file(GLOB SOURCES "*.cu" "*.cpp" "*.c")
file(GLOB HEADERS "*.h" "*.hpp" "*.cuh")

add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS})

find_package(CUDAToolkit REQUIRED)

# Set CUDA arch explicitly
set_target_properties(${PROJECT_NAME} PROPERTIES
        CUDA_ARCHITECTURES "86"
)

target_compile_options(${PROJECT_NAME} PRIVATE
        $<$<COMPILE_LANGUAGE:CUDA>:--expt-relaxed-constexpr>
        $<$<COMPILE_LANGUAGE:CUDA>:--extended-lambda>
)

target_link_libraries(${PROJECT_NAME} PRIVATE
        CUDA::cudart
)

target_include_directories(${PROJECT_NAME} PRIVATE
        ${CMAKE_CUDA_TOOLKIT_INCLUDE_DIRECTORIES}
        /usr/local/cccl/thrust
        /usr/local/cccl/cub
        /usr/local/cccl/libcudacxx/include
)