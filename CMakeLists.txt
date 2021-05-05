# project
cmake_minimum_required (VERSION 3.9)
project (libelas)

if (CMAKE_GENERATOR MATCHES "Visual Studio")
    # set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std:c++17")
    # set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -std:c++17")
    set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS YES)
else()
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra")
    set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -Wall -Wextra -DDEBUG")
endif()

option(elas_profiler "if on, elas profiler is used." OFF)

find_package(OpenCV 4 REQUIRED)

set(SOURCE_FILES
    src/elas.cpp
    src/filter.cpp
    src/matrix.cpp
    src/triangle.cpp
    src/descriptor.cpp
)

set(INCLUDE_DIRS include)

add_library(elas SHARED ${SOURCE_FILES})
target_include_directories(elas SYSTEM
    PUBLIC ${INCLUDE_DIRS}
    PUBLIC ${OPENCV_INCLUDE_DIRS}
)
target_link_libraries(elas
    PUBLIC ${OpenCV_LIBS}
)
target_compile_options(elas PRIVATE "-msse3")
if(elas_profiler)
    target_compile_definitions(elas PUBLIC -DPROFILE=true)
endif()

# build demo program
add_executable(example EXCLUDE_FROM_ALL src/main.cpp)
target_link_libraries(example
    PRIVATE elas
)
target_compile_options(example PRIVATE "-msse3")
