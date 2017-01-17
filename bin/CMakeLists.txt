# Add the sources that only the binary needs
set(UNRAR_SOURCES ${UNRAR_SOURCES} ${BIN_SPECIFIC_SOURCES})

# Add the definition that lets the source know this is the binary
add_definitions(-DUNRAR)

# Create the binary from the sources
add_executable(unrar-bin ${UNRAR_SOURCES})

# Set the output name to unrar.
# The reason the executable is unrar-bin is because there'd be a target name conflict
# between the bin and lib
set_target_properties(unrar-bin PROPERTIES OUTPUT_NAME unrar)

# Link against whatever threads library is present
find_package(Threads REQUIRED)
if (Threads_FOUND)
    target_link_libraries(unrar-bin ${CMAKE_THREAD_LIBS_INIT})
endif ()

install(TARGETS unrar-bin
        DESTINATION bin)