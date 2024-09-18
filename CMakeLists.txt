cmake_minimum_required(VERSION 3.27)
project(spdlog VERSION 1.0 LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(spdlog INTERFACE)

target_include_directories(spdlog
  INTERFACE
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include/spdlog>
)

include(CMakePackageConfigHelpers)
configure_package_config_file(
  "${CMAKE_CURRENT_SOURCE_DIR}/spdlogConfig.cmake.in"
  "${CMAKE_CURRENT_BINARY_DIR}/spdlogConfig.cmake"
  INSTALL_DESTINATION share/spdlog
)

install(TARGETS spdlog
  EXPORT spdlogTargets
  ARCHIVE DESTINATION lib
  LIBRARY DESTINATION lib
  RUNTIME DESTINATION bin
)

install(DIRECTORY ${CMAKE_SOURCE_DIR}/include/spdlog DESTINATION include/spdlog)

install(
  EXPORT spdlogTargets
  DESTINATION share/spdlog
  NAMESPACE spdlog::
)

install(
  FILES
  "${CMAKE_CURRENT_BINARY_DIR}/spdlogConfig.cmake"
  DESTINATION share/spdlog
)