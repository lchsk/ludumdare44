CMAKE_MINIMUM_REQUIRED(VERSION 2.8)

# Name of the project
project(condottiero)

# Set default build type to Debug
if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Debug CACHE STRING "Choose the build type (Debug or Release)" FORCE)
endif()

message(STATUS "CMake build type: " ${CMAKE_BUILD_TYPE})

# Version of the project
set(PROJECT_VERSION "1.0.0")

# If build type is Debug, generate debugging information and don't optimise
if (CMAKE_BUILD_TYPE STREQUAL Debug)
  add_definitions(-O0)
  set(CMAKE_C_FLAGS "-g -Wall -pedantic")
else()
  add_definitions(-O3)
  set(CMAKE_C_FLAGS "-Wall -pedantic")
endif()

# C standard for the compiler to use
set(CMAKE_CXX_STANDARD 17)

add_executable(
  condottiero

  # Game
  src/main.cpp

  # Libs
  lib/hex.cpp
  lib/animation.cpp
  lib/loader.cpp
  lib/hex_map.cpp
  lib/pathfinding.cpp
  lib/gui/gui.cpp
  lib/game.cpp
  )


############################################
#                                          #
#              Dependencies                #
#                                          #
############################################

find_package(PkgConfig)

pkg_check_modules(PKG_CONFIG "pkg-config")

pkg_check_modules(SFML sfml-all REQUIRED)
include_directories(
  ${SFML_INCLUDE_DIRS}
  )

link_directories(
  ${SFML_LIBRARY_DIRS}
  )

add_definitions(
  ${SFML_CXXFLAGS_OTHER}
  )

target_link_libraries(condottiero
  ${SFML_LIBRARIES}
  )
