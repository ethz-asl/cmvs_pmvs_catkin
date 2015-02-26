cmake_minimum_required(VERSION 2.8.3)
project(cmvs_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple(ALL_DEPS_REQUIRED)


# GRACLUS

add_definitions(-DNUMBITS=64)

include_directories(thirdparty/graclus1.2/multilevelLib thirdparty/graclus1.2/metisLib)

file(GLOB GRACLUS_LIB thirdparty/graclus1.2/metisLib/*.c)
file(GLOB MULTILEVEL_LIB thirdparty/graclus1.2/multilevelLib/*.c)
cs_add_library(graclus_lib ${GRACLUS_LIB} ${MULTILEVEL_LIB})


# CMVS

set(BASE_CMVS base_cmvs)
set(CMVS cmvs)

set(CMVS_LIBRARIES graclus_lib)

cs_add_library(${BASE_CMVS}	src/cmvs/bundle.cc
				src/cmvs/graclus.cc)
target_link_libraries(${BASE_CMVS} ${CMVS_LIBRARIES})

cs_add_executable(${CMVS} src/cmvs.cc)
target_link_libraries(${CMVS} ${BASE_CMVS})

cs_install()
cs_export()