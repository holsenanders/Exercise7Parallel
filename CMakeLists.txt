cmake_minimum_required(VERSION 3.18)

# Must come before project() so CMake finds nvcc even if it's not on PATH
set(CMAKE_CUDA_COMPILER /usr/local/cuda/bin/nvcc)

project(wave2d LANGUAGES CUDA)

set(CMAKE_CUDA_STANDARD 17)
set(CMAKE_CUDA_ARCHITECTURES sm_75)   # set to your GPU, see below

add_executable(parallel wave_2d_parallel.cu)

# Your flags: -fmad=false always, -O2 for Release, -g -G for Debug
target_compile_options(parallel PRIVATE
        -fmad=false
        $<$<CONFIG:Release>:-O2>
        $<$<CONFIG:Debug>:-g -G -O0>
)

target_link_libraries(parallel PRIVATE m)