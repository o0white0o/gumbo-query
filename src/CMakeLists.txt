# libgumbo_query

file(GLOB HEADERS_FILES 
		*.h
		)

file(INSTALL ${HEADERS_FILES} DESTINATION ${CMAKE_BINARY_DIR}/include/gq)
		
file(GLOB SOURCES_FILES 
		*.cpp
		)

add_library(gq STATIC
        ${HEADERS_FILES}
        ${SOURCES_FILES}
        )

target_link_libraries(gq
        PUBLIC
        gumbo
        )

target_include_directories(gq
        PUBLIC
        $<BUILD_INTERFACE:${CMAKE_BINARY_DIR}/include>
        $<INSTALL_INTERFACE:include>
		# For support include different way. (gq/Document.h or Document.h)
		$<BUILD_INTERFACE:${CMAKE_BINARY_DIR}/include/gq>
        $<INSTALL_INTERFACE:include/gq>
        )

install(FILES ${HEADERS_FILES} 
		DESTINATION ${CMAKE_INSTALL_PREFIX}/include/gq
        )

install(TARGETS gq
        EXPORT "${TARGETS_EXPORT_NAME}"
        LIBRARY DESTINATION "lib"
        ARCHIVE DESTINATION "lib"
        RUNTIME DESTINATION "bin"
        INCLUDES DESTINATION "include/gq"
        )
