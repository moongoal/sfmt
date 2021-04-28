cmake_minimum_required(VERSION 3.20)

project(
    sfmt
    VERSION 1.5.1
    DESCRIPTION "SIMD-oriented Fast Mersenne Twister"
    HOMEPAGE_URL http://www.math.sci.hiroshima-u.ac.jp/m-mat/MT/SFMT/
)

add_library(sfmt STATIC SFMT.c)

target_compile_options(
    sfmt
    PRIVATE
        -Wall -Wmissing-prototypes
        -O3 -finline-functions -fomit-frame-pointer -DNDEBUG
        -fno-strict-aliasing --param max-inline-insns-single=1800
        -msse2
)

target_compile_definitions(
    sfmt
    PRIVATE
        -DHAVE_SSE2
)

install(
    TARGETS sfmt
    ARCHIVE
)

file(
    GLOB SFMT_HEADERS
    LIST_DIRECTORIES false
    *.h
)

install(
    FILES ${SFMT_HEADERS}
    DESTINATION include/sfmt
)
