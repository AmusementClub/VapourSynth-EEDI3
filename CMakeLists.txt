cmake_minimum_required(VERSION 3.20.0)

project(EEDI3 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
set(CMAKE_INTERPROCEDURAL_OPTIMIZATION ON)
add_compile_definitions(EEDI3_X86)
add_compile_options(-fno-math-errno -fno-trapping-math)

add_library(eedi3m SHARED
    EEDI3/EEDI3.cpp
    EEDI3/vectorclass/instrset_detect.cpp
)
target_compile_options(eedi3m PRIVATE -march=x86-64-v2)

add_library(sse4 STATIC EEDI3/EEDI3_SSE4.cpp)
target_compile_options(sse4 PRIVATE -march=x86-64-v2)
target_link_libraries(eedi3m sse4)

add_library(avx2 STATIC EEDI3/EEDI3_AVX2.cpp)
target_compile_options(avx2 PRIVATE -march=x86-64-v3)
target_link_libraries(eedi3m avx2)

