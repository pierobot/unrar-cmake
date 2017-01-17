# Add the sources that only the binary needs
set(UNRAR_SOURCES ${UNRAR_SOURCES} ${BIN_SPECIFIC_SOURCES})

# Add the definition that lets the source know this is the binary
add_definitions(-DUNRAR)

# Create the binary from the sources
add_executable(unrar-bin ${UNRAR_SOURCES})

# Link against whatever threads library is present
find_package(Threads REQUIRED)
if (Threads_FOUND)
    target_link_libraries(unrar-bin ${CMAKE_THREAD_LIBS_INIT})
endif ()
