cmake_minimum_required(VERSION 3.28.3)
project(hello_world)

# add_executable(${PROJECT_NAME} Main.cpp Hello.cpp)
# Or we can
# Our Project
set(SOURCE_FILES
    Main.cpp
    Hello.cpp)


add_executable(${PROJECT_NAME} ${SOURCE_FILES})