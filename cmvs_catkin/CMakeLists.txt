cmake_minimum_required(VERSION 2.8.3)
project(cmvs_catkin)

find_package(catkin_simple REQUIRED)
catkin_simple(ALL_DEPS_REQUIRED)


# GRACLUS
if(CMAKE_SIZEOF_VOID_P EQUAL 8)
  add_definitions(-DNUMBITS=64)
endif(CMAKE_SIZEOF_VOID_P EQUAL 8)

include_directories(thirdparty/graclus1.2/multilevelLib
                    thirdparty/graclus1.2/metisLib)

# The graclus library declares these for external variables
# that are then defined in CMVS. On OSX undefined external
# symbols raise a linker error by default.
# See: http://glandium.org/blog/?p=2764
if(APPLE)
  set(UNDEF_SYMBOL_1 "-Wl,-U,_boundary_points")
  set(UNDEF_SYMBOL_2 "-Wl,-U,_spectral_initialization")
  set(UNDEF_SYMBOL_3 "-Wl,-U,_cutType")
  set(UNDEF_SYMBOL_4 "-Wl,-U,_memory_saving")
  set(CMAKE_SHARED_LINKER_FLAGS "${UNDEF_SYMBOL_1} \
                                ${UNDEF_SYMBOL_2} \
                                ${UNDEF_SYMBOL_3} \
                                ${UNDEF_SYMBOL_4}")
endif(APPLE)

file(GLOB GRACLUS_METIS_LIB_C thirdparty/graclus1.2/metisLib/*.c)
file(GLOB MULTILEVEL_LIB thirdparty/graclus1.2/multilevelLib/*.c)
cs_add_library(graclus_lib ${GRACLUS_METIS_LIB_C} ${MULTILEVEL_LIB})

# CMVS BASE
file(GLOB CMVS_LIB_CC src/cmvs/*.cc)
cs_add_library(base_cmvs ${CMVS_LIB_CC})
target_link_libraries(base_cmvs graclus_lib)

# CMVS
cs_add_executable(cmvs src/cmvs.cc)
target_link_libraries(cmvs base_cmvs graclus_lib)

cs_install()
cs_export()