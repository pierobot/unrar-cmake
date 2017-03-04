# unrar-cmake
CMake project for unrar and libunrar

### How do I include this in my project?
Clone this repository into your thirdparty directory.

```cmake
# CMakeLists.txt
set(CMAKE_MODULE_PATH "${CMAKE_MODULE_PATH} thirdparty/unrar-cmake/cmake/modules")

find_package(libunrar REQUIRED)
if (LIBUNRAR_FOUND)
  target_include_directories(mytarget PUBLIC ${LIBUNRAR_INCLUDE_DIR})
  target_link_libraries(mytarget ${LIBUNRAR_LIBRARY})
endif()
```
