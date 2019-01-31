cmake_minimum_required(VERSION 3.10)
project(nanovg)

add_library(nanovg STATIC
    src/nanovg.c
)

set(public_headers
          nanovg.h
          nanovg_gl.h
)

add_library(nanovg::nanovg ALIAS nanovg)

#target_compile_definitions(${PROJECT_NAME} PRIVATE FONS_USE_FREETYPE=1)

set_target_properties(nanovg
    PROPERTIES
        PUBLIC_HEADER "${public_headers}"
        POSITION_INDEPENDENT_CODE ON)

install(TARGETS nanovg EXPORT nanovgTargets
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    RUNTIME DESTINATION bin
    INCLUDES DESTINATION include/nanovg
    PUBLIC_HEADER DESTINATION include/nanovg
    )

install (EXPORT nanovgTargets
    FILE nanovgConfig.cmake
    NAMESPACE nanovg::
    DESTINATION lib/cmake/nanovg
    )