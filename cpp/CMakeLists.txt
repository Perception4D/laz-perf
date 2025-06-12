
file(GLOB SRCS
    lazperf/*.cpp
    lazperf/detail/*.cpp
)

lazperf_add_library(lazperf ${SRCS})

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

