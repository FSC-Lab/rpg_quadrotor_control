cmake_minimum_required(VERSION 3.14.0)
project(autopilot)

# Compile as C++11, supported in ROS Kinetic and newer
add_compile_options(-std=c++11)
add_compile_options(-O3)

find_package(Eigen3 REQUIRED)
find_package(
  catkin REQUIRED
  COMPONENTS geometry_msgs
             nav_msgs
             position_controller
             quadrotor_common
             quadrotor_msgs
             roscpp
             state_predictor
             std_msgs
             trajectory_generation_helper)

catkin_package(
  INCLUDE_DIRS
  include
  LIBRARIES
  autopilot_helper
  CATKIN_DEPENDS
  geometry_msgs
  nav_msgs
  position_controller
  quadrotor_common
  quadrotor_msgs
  roscpp
  state_predictor
  std_msgs
  trajectory_generation_helper
  DEPENDS
  Eigen3)

add_executable(autopilot src/autopilot_node.cpp)
target_include_directories(autopilot PRIVATE include ${catkin_INCLUDE_DIRS})
target_link_libraries(autopilot PRIVATE ${catkin_LIBRARIES} Eigen3::Eigen)

add_library(autopilot_helper src/autopilot_helper.cpp)
target_include_directories(autopilot_helper PUBLIC include
                                                   ${catkin_INCLUDE_DIRS})
target_link_libraries(autopilot_helper PUBLIC ${catkin_LIBRARIES} Eigen3::Eigen)
