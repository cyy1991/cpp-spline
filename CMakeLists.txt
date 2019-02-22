cmake_minimum_required(VERSION 2.8.3)
project(cpp-spline)

## Compile as C++11, supported in ROS Kinetic and newer
# add_compile_options(-std=c++11)

## Find catkin macros and libraries
## if COMPONENTS list like find_package(catkin REQUIRED COMPONENTS xyz)
## is used, also find other catkin packages
find_package(catkin REQUIRED COMPONENTS
  roscpp
  rospy
  std_msgs
)

## System dependencies are found with CMake's conventions
#find_package(Boost REQUIRED COMPONENTS system)


catkin_package(
   INCLUDE_DIRS include
#  LIBRARIES cpp-spline
  CATKIN_DEPENDS roscpp rospy std_msgs
#  DEPENDS system_lib
)

include_directories(
 include/cpp-spline/
  ${catkin_INCLUDE_DIRS}
)

add_library(bezier_node src/Bezier.cpp src/Curve.cpp src/Vector.cpp)
add_dependencies(bezier_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(bezier_node
    ${catkin_LIBRARIES}
    )

add_library(bspline_node src/BSpline.cpp src/Curve.cpp src/Vector.cpp)
add_dependencies(bspline_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(bspline_node
    ${catkin_LIBRARIES}
    )

add_library(catmullRom_node src/CatmullRom.cpp src/Curve.cpp src/Vector.cpp)
add_dependencies(catmullRom_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})
target_link_libraries(catmullRom_node
    ${catkin_LIBRARIES}
    )

add_executable(debug_spline_node test/src/main.cpp)
add_dependencies(debug_spline_node ${${PROJECT_NAME}_EXPORTED_TARGETS}  ${catkin_EXPORTED_TARGETS})
target_link_libraries(debug_spline_node
    ${catkin_LIBRARIES}
)
