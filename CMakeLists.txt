cmake_minimum_required(VERSION 3.27)

project(DemoAdd VERSION 0.1 LANGUAGES CXX)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

file(GLOB PROJECT_SOURCES
  ${PROJECT_SOURCE_DIR}/*.cpp
  ${PROJECT_SOURCE_DIR}/*.h)

add_library(DemoAdd ${PROJECT_SOURCES})

install(TARGETS DemoAdd
  EXPORT demo-vcpkg-lib-targets
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

install(
  EXPORT demo-vcpkg-lib-targets
  DESTINATION share/demo-vcpkg-lib
  NAMESPACE demo-vcpkg-lib::
)