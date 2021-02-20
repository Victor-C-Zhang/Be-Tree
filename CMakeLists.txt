cmake_minimum_required(VERSION 3.1)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS ON)

project(Be-Tree)

if("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
  message("Adding GNU compiler flags")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -W -Wall")
elseif("${CMAKE_CXX_COMPILER_ID}" STREQUAL "MSVC")
  message("Adding MSVC compiler flags")
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /Wall")
else()
  message("${CMAKE_CXX_COMPILER_ID} not recognized, no flags added")
endif()

add_executable(test
    test.cpp
    backing_store.cpp
    swap_space.cpp)
# optimize unless debug
if (DEFINED ENV{DEBUG})
  message("Disabling optimizations and enabling debug symbols")
  target_compile_options(test PRIVATE -g)
else ()
  if("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
    target_compile_options(test PRIVATE -O3)
  elseif("${CMAKE_CXX_COMPILER_ID}" STREQUAL "MSVC")
    target_compile_options(test PRIVATE /O2)
  endif()
endif ()