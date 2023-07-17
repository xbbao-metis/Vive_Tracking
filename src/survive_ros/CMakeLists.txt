cmake_minimum_required(VERSION 3.16)

project(survive_ros)
add_compile_options(-std=c++14)

#if(NOT TARGET survive)
#  message("Adding base cmake...")
#  set_property(GLOBAL PROPERTY SURVIVE_IN_CATKIN_MAKE On)
#  add_subdirectory(../../ survive_build)
#endif()

find_package(catkin REQUIRED COMPONENTS 
  roscpp
  geometry_msgs tf
  )

## System dependencies are found with CMake's conventions
# find_package(Boost REQUIRED COMPONENTS system)

###########
## Build ##
###########

## Specify additional locations of header files
## Your package locations should be listed before other locations
include_directories(
  libsurvive/include/libsurvive
#  libsurvive/src
  libsurvive/redist  
  libsurvive/libs/cnkalman/libs/cnmatrix/include
  ${catkin_INCLUDE_DIRS}
)

###################################
## catkin specific configuration ##
###################################
## The catkin_package macro generates cmake config files for your package
## Declare things to be passed to dependent projects
## INCLUDE_DIRS: uncomment this if your package contains header files
## LIBRARIES: libraries you create in this project that dependent projects also need
## CATKIN_DEPENDS: catkin_packages dependent projects also need
## DEPENDS: system dependencies of this project that dependent projects also need

link_directories(libsurvive/bin)
add_subdirectory(libsurvive)
#add_dependencies(survive_ros_node ${${PROJECT_NAME}_EXPORTED_TARGETS} ${catkin_EXPORTED_TARGETS})

## Rename C++ executable without prefix
## The above recommended prefix causes long target names, the following renames the
## target back to the shorter version for ease of user use
## e.g. "rosrun someones_pkg node" instead of "rosrun someones_pkg someones_pkg_node"
#set_target_properties(${PROJECT_NAME}_node PROPERTIES OUTPUT_NAME node PREFIX "")

## Declare a C++ executable
## With catkin_make all packages are built within a single CMake context
## The recommended prefix ensures that target names across packages don't collide
add_executable(survive_ros_node main.cc)
## Add cmake target dependencies of the executable
## same as for the library above


# Specify libraries to link a library or executable target against
target_link_libraries(survive_ros_node
    survive
    #libsurvive/bin
    ${catkin_LIBRARIES}
  )

## Mark executables and/or libraries for installation
# install(TARGETS ${PROJECT_NAME}
#   ARCHIVE DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   LIBRARY DESTINATION ${CATKIN_PACKAGE_LIB_DESTINATION}
#   RUNTIME DESTINATION ${CATKIN_PACKAGE_BIN_DESTINATION}
#)

# Mark cpp header files for installation
#install(DIRECTORY ../../include/libsurvive
#   DESTINATION ${CATKIN_PACKAGE_INCLUDE_DESTINATION}
#   FILES_MATCHING PATTERN "*.h"
#   PATTERN ".svn" EXCLUDE
# )

catkin_package()