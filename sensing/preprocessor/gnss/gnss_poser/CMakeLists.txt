cmake_minimum_required(VERSION 3.5)
project(gnss_poser)

### Compile options
if(NOT CMAKE_CXX_STANDARD)
  set(CMAKE_CXX_STANDARD 14)
endif()
if(CMAKE_COMPILER_IS_GNUCXX OR CMAKE_CXX_COMPILER_ID MATCHES "Clang")
  add_compile_options(-Wno-unused-parameter -Wall -Wextra -Wpedantic)
endif()

find_package(ament_cmake_auto)
ament_auto_find_build_dependencies()

set(GNSS_POSER_HEADERS
  include/gnss_poser/convert.hpp
  include/gnss_poser/gnss_poser_core.hpp
  include/gnss_poser/gnss_stat.hpp
 )

ament_auto_add_library(gnss_poser_node SHARED 
	src/gnss_poser_core.cpp 
	${GNSS_POSER_HEADERS}
)

rclcpp_components_register_node(gnss_poser_node
  PLUGIN "GNSSPoser"
  EXECUTABLE gnss_poser
)

ament_auto_package(INSTALL_TO_SHARE
  launch
)
