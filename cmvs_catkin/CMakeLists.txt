cmake_minimum_required(VERSION 2.8.3)
project(cmvs_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple(ALL_DEPS_REQUIRED)

find_package(LAPACK REQUIRED)
find_package(BLAS REQUIRED)
find_package(Boost REQUIRED)
find_package(JPEG REQUIRED)
find_package(Threads REQUIRED)

link_directories(thirdparty/graclus1.2 thirdparty/graclus1.2/metisLib)
include_directories(thirdparty/graclus1.2 thirdparty/graclus1.2/multilevelLib thirdparty/graclus1.2 thirdparty/graclus1.2/metisLib)


# GRACLUS

add_definitions(-DNUMBITS=64)

file(GLOB GRACLUS_LIB thirdparty/graclus1.2/metisLib/*.c)
file(GLOB MULTILEVEL_LIB thirdparty/graclus1.2/multilevelLib/*km.c)
cs_add_library(graclus_lib ${GRACLUS_LIB}
							 ${MULTILEVEL_LIB})


# CMVS

set(BASE_CMVS base_cmvs)
set(CMVS cmvs)

set(CMVS_LIBRARIES Xext X11 jpeg blas lapack multilevel metis m graclus_lib ${CMAKE_THRE/home/marius/catkin_ws/src/cmvs_pmvs2/thirdparty/tinycthread_catkin/includeAD_LIBS_INIT})

cs_add_library(${BASE_CMVS}	src/cmvs/bundle.cc
				src/cmvs/graclus.cc)
target_link_libraries(${BASE_CMVS} ${CMVS_LIBRARIES})

cs_add_executable(${CMVS} src/cmvs.cc)
target_link_libraries(${CMVS} ${BASE_CMVS})

cs_install()
cs_export()


