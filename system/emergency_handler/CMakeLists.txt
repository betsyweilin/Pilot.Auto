cmake_minimum_required(VERSION 3.5)
project(emergency_handler)

### Compile options
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()
if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wno-unused-parameter -Wall -Wextra -Wpedantic)
endif()

### Dependencies
find_package(ament_cmake_auto REQUIRED)
ament_auto_find_build_dependencies()

### Target executable
set(EMERGENCY_HANDLER_SRC
  src/emergency_handler_core.cpp)

set(EMERGENCY_HANDLER_HEADERS
  include/emergency_handler/emergency_handler_core.hpp)

ament_auto_add_executable(${PROJECT_NAME}
  src/emergency_handler_node.cpp
  ${EMERGENCY_HANDLER_SRC}
  ${EMERGENCY_HANDLER_HEADERS}
)

ament_auto_package(INSTALL_TO_SHARE
  launch
  config
)
