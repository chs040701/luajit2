cmake_minimum_required(VERSION 3.0...4.0)

if (IOS)
  set(CMAKE_SYSTEM_NAME Darwin CACHE STRING "Target platform for macOS")
  set(CMAKE_OSX_SYSROOT "/Library/Developer/CommandLineTools/SDKs/MacOSX.sdk" CACHE PATH "macOS SDK path" FORCE)
  set(CMAKE_OSX_ARCHITECTURES "arm64" CACHE STRING "Target architecture for macOS" FORCE)
  set(CMAKE_OSX_DEPLOYMENT_TARGET "10.15" CACHE STRING "Minimum macOS deployment version" FORCE)
endif()

project(minilua)

set(CMAKE_POSITION_INDEPENDENT_CODE OFF)

find_library(LIBM_LIBRARIES NAMES m)

add_executable(minilua ../../minilua.c)
if (LIBM_LIBRARIES)
  target_link_libraries(minilua ${LIBM_LIBRARIES})
endif()

if (MSVC)
  set_target_properties(minilua PROPERTIES RUNTIME_OUTPUT_DIRECTORY $<1:${CMAKE_CURRENT_BINARY_DIR}>)
endif()
