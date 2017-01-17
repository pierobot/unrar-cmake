# Add the sources that only the binary needs
set(UNRAR_SOURCES ${UNRAR_SOURCES} ${LIB_SPECIFIC_SOURCES})

# Add the definitions specific for the library
add_definitions(-DRARDLL
                -DUNRAR
                -DSILENT)

# Choose between static and shared based on user input
if (BUILD_STATIC)
    add_library(unrar STATIC ${UNRAR_SOURCES})
else ()
    add_library(unrar SHARED ${UNRAR_SOURCES})
endif ()

# Link against whatever threads library is present
find_package(Threads REQUIRED)
if (Threads_FOUND)
    target_link_libraries(unrar ${CMAKE_THREAD_LIBS_INIT})
endif ()

install(TARGETS unrar
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)

install(FILES ${LIB_SPECIFIC_HEADERS} 
        DESTINATION include/unrar)

# Seems to be common?
if (INSTALL_HEADERS_TO_ROOT)
    install(FILES ${LIB_SPECIFIC_HEADERS} 
            DESTINATION include)
endif ()
