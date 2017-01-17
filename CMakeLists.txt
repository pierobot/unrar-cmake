cmake_minimum_required(VERSION 2.8.12)

project(unrar-cmake CXX)

option(BIN_ONLY "If set to ON, then only the binary will be built.")
option(LIB_ONLY "If set to ON, then only the library will be built.")
option(BUILD_STATIC "If set to ON, a static library will be built.")
option(INSTALL_HEADERS_TO_ROOT "If set to ON, dll.hpp and version.hpp will be copied directly to the root of your include directory.")

if (${CMAKE_CXX_COMPILER_ID} STREQUAL "MSVC")
    add_definitions(-D_SCL_SECURE_NO_WARNINGS
                    -D_CRT_SECURE_NO_WARNINGS
                    -DWIN32_LEAN_AND_MEAN)
    set(CMAKE_USE_WIN32_THREADS_INIT TRUE)
else ()
    # raros.hpp takes care of this definitiom for the library.
    #add_definitions(-D_UNIX)
    # However, applications using unrar that are not for Windows MUST define _UNIX
    add_definitions(-D_FILE_OFFSET_BITS=64
                    -D_LARGEFILE_SOURCE
                    -DRAR_SMP)
endif ()

include_directories(${CMAKE_SOURCE_DIR}/thirdparty/unrar)

set(LIB_SPECIFIC_SOURCES
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/dll.cpp)
set(LIB_SPECIFIC_HEADERS
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/dll.hpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/version.hpp)

set(BIN_SPECIFIC_SOURCES
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/recvol.cpp)

set(UNRAR_SOURCES
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/rar.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/scantree.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/qopen.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/cmddata.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/rs.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/rs16.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/filestr.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/strlist.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/strfn.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/pathfn.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/smallfn.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/global.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/file.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/filefn.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/filcreat.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/archive.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/arcread.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/unicode.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/system.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/isnt.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/crypt.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/crc.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/rawread.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/encname.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/resource.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/match.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/timefn.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/rdwrfn.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/consio.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/options.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/errhnd.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/rarvm.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/secpassword.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/rijndael.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/getbits.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/sha1.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/sha256.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/blake2s.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/hash.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/extinfo.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/extract.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/volume.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/list.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/find.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/unpack.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/headers.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/threadpool.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/rs16.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/cmddata.cpp
    ${CMAKE_SOURCE_DIR}/thirdparty/unrar/ui.cpp
)

if (BIN_ONLY)
    add_subdirectory(bin)
elseif (LIB_ONLY)
    add_subdirectory(lib)
else ()
    add_subdirectory(bin)
    add_subdirectory(lib)
endif ()
