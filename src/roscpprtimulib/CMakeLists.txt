cmake_minimum_required(VERSION 2.8.3)
project(roscpprtimulib)

find_package(catkin REQUIRED COMPONENTS
  roscpp
  sensor_msgs
)

catkin_package(
    LIBRARIES roscpprtimulib
    CATKIN_DEPENDS roscpp sensor_msgs
)

include_directories(
  ${catkin_INCLUDE_DIRS}
)

add_executable(roscpprtimulib src/roscpprtimulib.cpp)

target_link_libraries(roscpprtimulib
  ${catkin_LIBRARIES}
  RTIMULib
)
