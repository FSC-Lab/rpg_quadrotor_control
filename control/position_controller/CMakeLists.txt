cmake_minimum_required(VERSION 3.14.0)
project(position_controller)

# Compile as C++11, supported in ROS Kinetic and newer
add_compile_options(-std=c++11)
add_compile_options(-O3)

find_package(Eigen3 REQUIRED)
find_package(catkin REQUIRED COMPONENTS quadrotor_common roscpp)

catkin_package(
  INCLUDE_DIRS
  include
  LIBRARIES
  ${PROJECT_NAME}
  CATKIN_DEPENDS
  quadrotor_common
  roscpp
  DEPENDS
  Eigen3)

add_library(${PROJECT_NAME} src/position_controller.cpp)
target_include_directories(${PROJECT_NAME} PUBLIC include
                                                  ${catkin_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} PUBLIC Eigen3::Eigen ${catkin_LIBRARIES})
