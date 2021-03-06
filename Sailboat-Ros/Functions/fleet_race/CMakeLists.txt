cmake_minimum_required(VERSION 2.8.3)
project(fleet_race)

## Add support for C++11, supported in ROS Kinetic and newer
add_definitions(-std=c++11)

find_package(catkin REQUIRED COMPONENTS
        dynamic_reconfigure
        roscpp
        rospy
        sailboat_message
        std_msgs
        )


## Generate dynamic reconfigure parameters in the 'cfg' folder
generate_dynamic_reconfigure_options(
  cfg/fleet_race.cfg
#   cfg/DynReconf2.cfg
)

catkin_package(
        INCLUDE_DIRS include
        LIBRARIES fleet_race
        CATKIN_DEPENDS dynamic_reconfigure roscpp rospy sailboat_message std_msgs
        #DEPENDS system_lib
)

###########
## Build ##
###########
include_directories(
        include
        ${CMAKE_CURRENT_SOURCE_DIR}/include/${PROJECT_NAME}
        ${catkin_INCLUDE_DIRS})


set( fleet_race_SRC
        src/fleet_race_main.cpp
        src/race_course.cpp
        src/rt_nonfinite.cpp
        src/rtGetInf.cpp
        src/rtGetNaN.cpp
        )

add_executable( ${PROJECT_NAME} ${fleet_race_SRC} )
add_dependencies( ${PROJECT_NAME} ${catkin_EXPORTED_TARGETS} fleet_race_gencfg)
target_link_libraries( ${PROJECT_NAME} ${catkin_LIBRARIES} )
