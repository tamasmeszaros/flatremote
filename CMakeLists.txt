cmake_minimum_required(VERSION 3.14)

project(flatremote)

find_package(OpenGL REQUIRED)

find_package(wxWidgets 3.0 REQUIRED COMPONENTS gl core base)
include(${wxWidgets_USE_FILE})  

add_executable(flatremote main.cpp)

target_link_libraries(flatremote PRIVATE OpenGL::OpenGL ${wxWidgets_LIBRARIES})