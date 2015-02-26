cmake_minimum_required(VERSION 2.8.3)
project(tinycthread_catkin)

find_package(catkin_simple REQUIRED)
find_package(Threads REQUIRED)

catkin_simple(ALL_DEPS_REQUIRED)

cs_add_library(${PROJECT_NAME}	src/tinycthread.c
				src/rwmutex.cpp)
target_link_libraries(${PROJECT_NAME} ${CMAKE_THREAD_LIBS_INIT})

cs_install()
cs_export()


