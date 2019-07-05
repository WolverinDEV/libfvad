project(libfvad)
cmake_minimum_required(VERSION 3.8)

set(CMAKE_CXX_STANDARD 17)


option(BUILD_SHARED "Build shared libraries" ON)
option(BUILD_STATIC "Build static libraries" ON)

file(GLOB_RECURSE SOURCE_FILES src/*.c)
if (BUILD_SHARED)
    message("Building shared libraries")
    add_library(fvad_shared SHARED ${SOURCE_FILES})
    set_target_properties(fvad_shared PROPERTIES OUTPUT_NAME fvad)

    install(TARGETS fvad_shared
            ARCHIVE DESTINATION lib
            LIBRARY DESTINATION lib
    )
endif ()
if (BUILD_STATIC)
    message("Building static libraries")
    add_library(fvad_static STATIC ${SOURCE_FILES})
    set_target_properties(fvad_static PROPERTIES OUTPUT_NAME fvad)

    install(TARGETS fvad_static
            ARCHIVE DESTINATION lib
            LIBRARY DESTINATION lib
    )
endif ()

install(DIRECTORY include/ DESTINATION include/)