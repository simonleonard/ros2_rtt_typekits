cmake_minimum_required(VERSION 3.5)

project(kdl_typekit)

# Defines the orocos_* cmake macros. See that file for additional
# documentation.


find_package(ament_cmake REQUIRED)
ament_environment_hooks(env-hooks/kdl_typekit.sh.in)

find_package(rtt_ros2 REQUIRED)

find_package(orocos_kdl REQUIRED)
link_directories(${orocos_kdl_LIBRARY_DIRS})

include_directories(
  include/orocos
  ${orocos_kdl_INCLUDE_DIRS}
)

# Define the way rotation properties get written to XML
# Set one of the two options below to write them as EULER ZYX or RPY
# Set none of them to write them as matrices
#add_definitions(-DROTATION_PROPERTIES_EULER)
add_definitions(-DROTATION_PROPERTIES_RPY)

orocos_typekit(${PROJECT_NAME}
  src/kdlTypekit.cpp
  src/kdlTypekitConstructors.cpp
  src/kdlTypekitOperators.cpp
  src/kdlTypekitChain.cpp
  src/kdlTypekitFrame.cpp
  src/kdlTypekitJacobian.cpp
  src/kdlTypekitJntArray.cpp
  src/kdlTypekitJoint.cpp
  src/kdlTypekitRotation.cpp
  src/kdlTypekitSegment.cpp
  src/kdlTypekitTwist.cpp
  src/kdlTypekitVector.cpp
  src/kdlTypekitWrench.cpp
  src/motionproperties.cpp
  src/kinfamproperties.cpp
  )

target_link_libraries(${PROJECT_NAME} ${orocos_kdl_LIBRARIES})

add_subdirectory(src/corba)
add_subdirectory(src/mqueue)

if(CATKIN_ENABLE_TESTING)
  add_subdirectory(test)
endif()

file(GLOB LUA_FILES "lua/*.lua")


install(
  FILES ${LUA_FILES}
  DESTINATION share/lua/5.1/${PROJECT_NAME}/
)

orocos_install_headers(
  FILES include/orocos/${PROJECT_NAME}/typekit/Types.hpp
  INSTALL include/orocos/${PROJECT_NAME}/typekit
)

ament_package()

orocos_generate_package(
	INCLUDE_DIRS include
  DEPENDS_TARGET orocos-kdl
)
