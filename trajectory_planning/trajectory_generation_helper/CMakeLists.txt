cmake_minimum_required(VERSION 3.14.0)
project(trajectory_generation_helper)

# Compile as C++11, supported in ROS Kinetic and newer
add_compile_options(-std=c++11)
add_compile_options(-O3)

find_package(Eigen3 REQUIRED)
find_package(catkin REQUIRED COMPONENTS roscpp polynomial_trajectories
                                        quadrotor_common)

catkin_package(
  INCLUDE_DIRS
  include
  LIBRARIES
  ${PROJECT_NAME}
  CATKIN_DEPENDS
  roscpp
  polynomial_trajectories
  quadrotor_common)

add_library(
  ${PROJECT_NAME}
  src/polynomial_trajectory_helper.cpp src/heading_trajectory_helper.cpp
  src/circle_trajectory_helper.cpp)
target_include_directories(${PROJECT_NAME} PUBLIC include
                                                  ${catkin_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} PUBLIC ${catkin_LIBRARIES} Eigen3::Eigen)
