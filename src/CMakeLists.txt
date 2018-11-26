# libgumbo_query

file(GLOB SRC_FILES *.cpp)
file(GLOB HEAD_FILES *.h)
add_library(gq STATIC
        ${HEAD_FILES}
        ${SRC_FILES}
        )


target_link_libraries(gq
        PUBLIC
        gumbo
        )

file(INSTALL
        ${HEAD_FILES} DESTINATION
        ${CMAKE_BINARY_DIR}/include/gq
        )
target_include_directories(gq
        PUBLIC
        $<BUILD_INTERFACE:${CMAKE_BINARY_DIR}/include>
        $<INSTALL_INTERFACE:include>
        )

install(FILES
        ${HEAD_FILES} DESTINATION
        ${CMAKE_INSTALL_PREFIX}/include/gq
        )

install(TARGETS gq
        EXPORT "${TARGETS_EXPORT_NAME}"
        LIBRARY DESTINATION "lib"
        ARCHIVE DESTINATION "lib"
        RUNTIME DESTINATION "bin"
        INCLUDES DESTINATION "${CMAKE_INSTALL_PREFIX}/include/gq"
        )
