cmake_minimum_required(VERSION 3.11)
project(gumbo_query CXX)

add_subdirectory(dependency/gumbo-parser)
add_subdirectory(src)

option(BUILD_GUMBO_QUERY_TESTS "Builds gumbo-query tests" OFF)
if(BUILD_GUMBO_QUERY_TESTS)
		include(CTest)
        add_subdirectory(tests)
		enable_testing()
		add_test(NAME "ID Test" COMMAND id_test)
endif()
