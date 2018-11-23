project(gumbo_query CXX)
cmake_minimum_required(VERSION 3.8 FATAL_ERROR)

# Debug build.
set(CMAKE_VERBOSE_MAKEFILE ON)
set(CMAKE_BUILD_TYPE Debug)

# Set our output directories.
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/lib)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_LIBRARY_OUTPUT_DIRECTORY})

# Create library directory if it does not exist.
file(MAKE_DIRECTORY ${CMAKE_LIBRARY_OUTPUT_DIRECTORY})

add_subdirectory(dependency/gumbo-parser/)

# Library target.
add_library(gq STATIC
        # headers
        include/gq/Document.h
        include/gq/Node.h
        include/gq/Object.h
        include/gq/Parser.h
        include/gq/QueryUtil.h
        include/gq/Selector.h
        include/gq/Selection.h
        # sources
        src/Selector.cpp
        src/Selection.cpp
        src/QueryUtil.cpp
        src/Parser.cpp
        src/Object.cpp
        src/Node.cpp
        src/Document.cpp
        )

target_include_directories(gq PUBLIC
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>
        )

target_link_libraries(gq PUBLIC gumbo)

install(TARGETS gq
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib
        )

file(GLOB HEAD_FILES include/gq/*.h)
install(FILES
        ${HEAD_FILES} DESTINATION
        ${CMAKE_INSTALL_PREFIX}/include/gq
        )

