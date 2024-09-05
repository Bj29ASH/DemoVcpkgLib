cmake_minimum_required(VERSION 3.27)

project(DemoAdd VERSION 0.1 LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

file(GLOB PROJECT_SOURCES
  ${PROJECT_SOURCE_DIR}/*.cpp)

file(GLOB PROJECT_HEADERS
  ${PROJECT_SOURCE_DIR}/*.h)

add_library(DemoAdd STATIC ${PROJECT_SOURCES})

install(
  TARGETS DemoAdd
  EXPORT DemoAdd-targets
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

install(FILES ${PROJECT_HEADERS} DESTINATION "include/DemoAdd")

include(CMakePackageConfigHelpers)
configure_package_config_file(
  "${CMAKE_CURRENT_SOURCE_DIR}/DemoAdd-config.cmake.in"
  "${CMAKE_CURRENT_BINARY_DIR}/DemoAdd-config.cmake"
  INSTALL_DESTINATION "share/DemoAdd"
)

install(
  FILES "${CMAKE_CURRENT_BINARY_DIR}/DemoAdd-config.cmake"
  DESTINATION "share/DemoAdd"
)

install(
  EXPORT DemoAdd-targets
  DESTINATION share/DemoAdd
  NAMESPACE DemoAdd::
)