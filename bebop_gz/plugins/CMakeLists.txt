cmake_minimum_required(VERSION 3.10)
project(GazeboPlugins)

# Buscar dependencias de Gazebo Harmonic
find_package(gz-cmake3 REQUIRED)
find_package(gz-sim8 REQUIRED)
find_package(gz-transport13 REQUIRED)
find_package(gz-msgs10 REQUIRED)
find_package(gz-plugin2 REQUIRED)
find_package(gz-math7 REQUIRED)
find_package(gz-common5 REQUIRED)

# Habilitar C++17 (necesario para Harmonic)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Plugin 1: SetPosePlugin
add_library(SetPosePlugin SHARED SetPosePlugin.cc)
target_link_libraries(SetPosePlugin
  gz-sim8::gz-sim8
  gz-transport13::gz-transport13
  gz-msgs10::gz-msgs10
  gz-plugin2::gz-plugin2
  gz-math7::gz-math7
  gz-common5::gz-common5
)

# Plugin 2: RobotPosePublisher
add_library(RobotPosePublisher SHARED RobotPosePublisher.cc)
target_link_libraries(RobotPosePublisher
  gz-sim8::gz-sim8
  gz-transport13::gz-transport13
  gz-plugin2::gz-plugin2
  gz-math7::gz-math7
  gz-common5::gz-common5
)

# Instalar los plugins
install(TARGETS SetPosePlugin RobotPosePublisher
  LIBRARY DESTINATION lib
)

