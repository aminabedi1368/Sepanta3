cmake_minimum_required(VERSION 2.8.3)
project(k2_client)

## Find catkin and any catkin packages
find_package(catkin REQUIRED COMPONENTS
  sensor_msgs
  cv_bridge
  roscpp
  rospy
  genmsg
  pcl_conversions
  pcl_ros
  tf
  std_msgs
  nav_msgs
  geometry_msgs
  image_transport
  message_generation
  actionlib
  actionlib_msgs 
  dynamixel_msgs
  camera_info_manager
)

find_package(Boost COMPONENTS system thread date_time REQUIRED)
find_package(PkgConfig REQUIRED)
find_package(OpenCV 2.2 REQUIRED)
find_package(PkgConfig REQUIRED)
pkg_check_modules(EIGEN REQUIRED eigen3)

add_message_files(
    FILES 
    Activities.msg
    Appearance.msg
    Audio.msg
    Body.msg
    BodyArray.msg
    Expressions.msg
    JointOrientationAndType.msg
    JointPositionAndState.msg
    Lean.msg
)

generate_messages(
    DEPENDENCIES 
    std_msgs 
    geometry_msgs
)


catkin_package(
      INCLUDE_DIRS include 
      CATKIN_DEPENDS message_runtime
)

include_directories(include /usr/include/jsoncpp/ ${catkin_INCLUDE_DIRS} ${EIGEN_INCLUDE_DIRS} ${SERIAL_INCLUDE_DIRS} ${OpenCV_INCLUDE_DIRS}  ${JSONCPP_INCLUDE_DIR})


add_executable(startRGB src/startRGB.cpp)
target_link_libraries(startRGB ${catkin_LIBRARIES} ${Boost_LIBRARIES} /usr/lib/x86_64-linux-gnu/libjsoncpp.so)

add_executable(startIR src/startIR.cpp)
target_link_libraries(startIR ${catkin_LIBRARIES} ${Boost_LIBRARIES}  /usr/lib/x86_64-linux-gnu/libjsoncpp.so)

add_executable(startDepth src/startDepth.cpp)
target_link_libraries(startDepth ${catkin_LIBRARIES} ${Boost_LIBRARIES}  /usr/lib/x86_64-linux-gnu/libjsoncpp.so)

add_executable(startAudio src/startAudio.cpp)
target_link_libraries(startAudio ${catkin_LIBRARIES} ${Boost_LIBRARIES} /usr/lib/x86_64-linux-gnu/libjsoncpp.so)

add_executable(startBody src/startBody.cpp)
target_link_libraries(startBody ${catkin_LIBRARIES} ${Boost_LIBRARIES}  /usr/lib/x86_64-linux-gnu/libjsoncpp.so)

add_dependencies(startRGB ${PROJECT_NAME}_generate_messages_cpp sepanta_msgs_generate_messages_cpp)
add_dependencies(startIR ${PROJECT_NAME}_generate_messages_cpp sepanta_msgs_generate_messages_cpp)
add_dependencies(startDepth ${PROJECT_NAME}_generate_messages_cpp sepanta_msgs_generate_messages_cpp)
add_dependencies(startAudio ${PROJECT_NAME}_generate_messages_cpp sepanta_msgs_generate_messages_cpp)
add_dependencies(startBody ${PROJECT_NAME}_generate_messages_cpp sepanta_msgs_generate_messages_cpp)
