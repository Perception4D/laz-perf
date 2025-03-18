
file(GLOB SRCS
    lazperf/*.cpp
    lazperf/detail/*.cpp
)

set (LAZPERF_SHARED_LIB lazperf)
set (LAZPERF_STATIC_LIB lazperf_s)

if (NOT EMSCRIPTEN)
    lazperf_add_library(${LAZPERF_SHARED_LIB} SHARED ${SRCS})
endif()
lazperf_add_library(${LAZPERF_STATIC_LIB} STATIC ${SRCS})

file(GLOB HEADERS
    lazperf/*.hpp
)

file(GLOB HEADERS_DETAILS
    lazperf/detail/*.hpp
)

install(
    FILES
        ${HEADERS}
    DESTINATION
        include/lazperf
)

install(
    FILES
        ${HEADERS_DETAILS}
    DESTINATION
        include/lazperf/detail
)

install(
    FILES
        lazperf/lazperf_user_base.hpp
    DESTINATION
        include/lazperf
    RENAME
        lazperf_base.hpp
)

add_subdirectory(benchmarks)
add_subdirectory(tools)
if (EMSCRIPTEN)
    add_subdirectory(emscripten)
endif()

if (WITH_TESTS)
    enable_testing()
    add_subdirectory(test)
    add_subdirectory(examples)
endif()

