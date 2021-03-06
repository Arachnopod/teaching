cmake_minimum_required(VERSION 2.8.3)
project(uol_kobuki_gazebo_plugins)

find_package(gazebo REQUIRED)

find_package(catkin REQUIRED COMPONENTS gazebo_ros
                                        geometry_msgs
                                        kobuki_msgs
                                        nav_msgs
                                        roscpp
                                        sensor_msgs
                                        std_msgs
                                        tf)

catkin_package(INCLUDE_DIRS include
               LIBRARIES gazebo_ros_kobuki
               CATKIN_DEPENDS gazebo_ros
                              geometry_msgs
                              kobuki_msgs
                              nav_msgs
                              roscpp
                              sensor_msgs
                              std_msgs
                              tf)

link_directories(${GAZEBO_LIBRARY_DIRS})
include_directories(include
                    ${catkin_INCLUDE_DIRS}
                    ${GAZEBO_INCLUDE_DIRS})

add_library(uol_gazebo_ros_kobuki src/gazebo_ros_kobuki.cpp)
add_dependencies(uol_gazebo_ros_kobuki geometry_msgs_gencpp
                                   kobuki_msgs_gencpp
                                   nav_msgs_gencpp
                                   sensor_msgs_gencpp
                                   std_msgs_gencpp)
target_link_libraries(uol_gazebo_ros_kobuki
                      ${catkin_LIBRARIES}
                      ${GAZEBO_LIBRARIES})

install(TARGETS uol_gazebo_ros_kobuki
        DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION})
