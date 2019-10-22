project(BoostPythonExample)

cmake_minimum_required(VERSION 3.15)

find_package(Python3 COMPONENTS Interpreter Development)

find_package(Boost REQUIRED python)

message(STATUS "Python3_LIBRARIES = ${Python3_LIBRARIES}")
message(STATUS "Python3_EXECUTABLE = ${Python3_EXECUTABLE}")
message(STATUS "Python3_INCLUDE_DIRS = ${Python3_INCLUDE_DIRS}")
message(STATUS "Boost_LIBRARIES = ${Boost_LIBRARIES}")

enable_testing()

Python3_add_library(classes MODULE classes.cpp)
target_link_libraries(classes PRIVATE ${Boost_LIBRARIES} ${Python3_LIBRARIES})
target_include_directories(classes PRIVATE ${Boost_INCLUDE_DIRS} ${Python3_INCLUDE_DIRS})

file(COPY classes.py DESTINATION .)
add_test(NAME ExposingClasses COMMAND ${Python3_EXECUTABLE} classes.py)

