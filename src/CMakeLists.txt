# Library target.
add_library(gq STATIC
        # headers
        Document.h
        Node.h
        Object.h
        Parser.h
        QueryUtil.h
        Selector.h
        Selection.h
        # sources
        Selector.cpp
        Selection.cpp
        QueryUtil.cpp
        Parser.cpp
        Object.cpp
        Node.cpp
        Document.cpp
        )

find_package(Gumbo REQUIRED)
target_include_directories(gq PUBLIC
        ${Gumbo_INCLUDE_DIRS}/gumbo
        )

target_link_libraries(gq PRIVATE gumbo)

install(TARGETS gq
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)

file(GLOB HEAD_FILES *.h)
install(FILES ${HEAD_FILES} DESTINATION ${CMAKE_INSTALL_PREFIX}/include/gq)
file(INSTALL ${HEAD_FILES} DESTINATION ${CMAKE_INSTALL_PREFIX}/include/gq)