cmake_minimum_required(VERSION 3.14.0)
project(polynomial_trajectories)

# Compile as C++11, supported in ROS Kinetic and newer
add_compile_options(-std=c++11)
add_compile_options(-O3)

find_package(Eigen3 REQUIRED)
find_package(catkin REQUIRED COMPONENTS roscpp quadrotor_common quadrotor_msgs)

catkin_package(
  INCLUDE_DIRS
  include
  LIBRARIES
  ${PROJECT_NAME}
  CATKIN_DEPENDS
  roscpp
  quadrotor_common
  quadrotor_msgs
  DEPENDS
  Eigen3)

add_library(
  ${PROJECT_NAME}
  src/polynomial_trajectory.cpp src/polynomial_trajectories_common.cpp
  src/minimum_snap_trajectories.cpp src/constrained_polynomial_trajectories.cpp)

target_include_directories(${PROJECT_NAME} PUBLIC include
                                                  ${catkin_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} PUBLIC ${catkin_LIBRARIES} Eigen3::Eigen)
