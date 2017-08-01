cmake_minimum_required(VERSION 2.8.3)
project(gps_kf)

## Compile as C++11, supported in ROS Kinetic and newer
##add_compile_options(-std=c++98)
# rosbuild_remove_compile_flags

## Find catkin macros and libraries
find_package(catkin REQUIRED COMPONENTS
  geometry_msgs
  std_msgs
  tf2_ros
  cmake_modules
)

find_package(Eigen REQUIRED)

catkin_package(
  DEPENDS Eigen
)

include_directories(
  include
  ${catkin_INCLUDE_DIRS}
  ${Eigen_INCLUDE_DIRS}
)


add_executable(gpsKf_node src/gps_odom.cpp
                          src/filter.cpp)
target_link_libraries(gpsKf_node ${catkin_LIBRARIES})

#This makes sure that messages and services are compiled before the rest
add_dependencies(gpsKf_node gps_kf_generate_messages_cpp)
add_dependencies(gpsKf_node ${catkin_EXPORTED_TARGETS})
