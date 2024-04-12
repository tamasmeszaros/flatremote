cmake_minimum_required(VERSION 3.14)

project(flatremote)

find_package(OpenGL REQUIRED)

# set(wxWidgets_CONFIG_OPTIONS --toolkit=gtk3 )
find_package(wxWidgets 3.1 REQUIRED COMPONENTS gl core base)
include(${wxWidgets_USE_FILE})

add_executable(flatremote main.cpp)

target_link_libraries(flatremote PRIVATE OpenGL::GL ${wxWidgets_LIBRARIES})

install(TARGETS flatremote EXPORT FlatremoteTargets)

include(CMakePackageConfigHelpers)
write_basic_package_version_file(
  "${CMAKE_CURRENT_BINARY_DIR}/Flatremote/FlatremoteConfigVersion.cmake"
  VERSION 1.0
  COMPATIBILITY AnyNewerVersion
)

export(EXPORT FlatremoteTargets
  FILE "${CMAKE_CURRENT_BINARY_DIR}/Flatremote/FlatremoteTargets.cmake"
  NAMESPACE Flatremote::
)

file(WRITE ${CMAKE_CURRENT_BINARY_DIR}/FlatremoteConfig.cmake "include(\"\${CMAKE_CURRENT_LIST_DIR}/FlatremoteTargets.cmake\")")
set(ConfigPackageLocation lib/cmake/Flatremote)
install(EXPORT FlatremoteTargets
  FILE
  FlatremoteTargets.cmake
  NAMESPACE
    Flatremote::
  DESTINATION
    ${ConfigPackageLocation}
)
install(
  FILES
  ${CMAKE_CURRENT_BINARY_DIR}/FlatremoteConfig.cmake
    "${CMAKE_CURRENT_BINARY_DIR}/Flatremote/FlatremoteConfigVersion.cmake"
  DESTINATION
    ${ConfigPackageLocation}
  COMPONENT
    Devel
)