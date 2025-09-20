cmake_minimum_required(VERSION 3.20.0)

project(EEDI3 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)
add_compile_definitions(VS_TARGET_CPU_X86)
add_compile_options(-ffast-math)

add_library(eedi3m SHARED
    EEDI3/EEDI3.cpp
    EEDI3/EEDI3.hpp
    EEDI3/shared.hpp
    EEDI3/vectorclass/instrset.h
    EEDI3/vectorclass/instrset_detect.cpp
    EEDI3/EEDI3_SSE2.cpp
    EEDI3/vectorclass/vectorclass.h
    EEDI3/vectorclass/vectorf128.h
    EEDI3/vectorclass/vectorf256.h
    EEDI3/vectorclass/vectorf256e.h
    EEDI3/vectorclass/vectorf512.h
    EEDI3/vectorclass/vectorf512e.h
    EEDI3/vectorclass/vectori128.h
    EEDI3/vectorclass/vectori256.h
    EEDI3/vectorclass/vectori256e.h
    EEDI3/vectorclass/vectori512.h
    EEDI3/vectorclass/vectori512e.h
)
target_compile_options(eedi3m PRIVATE -march=x86-64-v3)

add_library(sse4 STATIC EEDI3/EEDI3_SSE4.cpp)
target_compile_options(sse4 PRIVATE -march=x86-64-v3)
target_link_libraries(eedi3m sse4)

add_library(avx STATIC EEDI3/EEDI3_AVX.cpp)
target_compile_options(avx PRIVATE -march=x86-64-v3)
target_link_libraries(eedi3m avx)

add_library(avx512 STATIC EEDI3/EEDI3_AVX512.cpp)
target_compile_options(avx512 PRIVATE -march=x86-64-v4)
target_link_libraries(eedi3m avx512)

