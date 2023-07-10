cmake_minimum_required(VERSION 3.14.0)
project(rpg_rotors_interface)

# Compile as C++11, supported in ROS Kinetic and newer
add_compile_options(-std=c++11)
add_compile_options(-O3)

find_package(catkin REQUIRED COMPONENTS mav_msgs nav_msgs quadrotor_common
                                        quadrotor_msgs roscpp std_srvs)

catkin_package(
  CATKIN_DEPENDS
  mav_msgs
  nav_msgs
  quadrotor_common
  quadrotor_msgs
  roscpp
  std_srvs)

add_executable(rpg_rotors_interface src/rpg_rotors_interface.cpp)
target_include_directories(rpg_rotors_interface PRIVATE include
                                                        ${catkin_INCLUDE_DIRS})
target_link_libraries(rpg_rotors_interface PRIVATE ${catkin_LIBRARIES})
