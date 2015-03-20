cmake_minimum_required(VERSION 2.8.3)
project(pmvs_catkin)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_SOURCE_DIR}/cmake)

find_package(catkin_simple REQUIRED)
catkin_simple(ALL_DEPS_REQUIRED)

find_package(Boost REQUIRED)
find_package(JPEG REQUIRED)
find_package(LAPACK REQUIRED)
find_package(Xext REQUIRED)
find_package(X11 REQUIRED)

include_directories(${X11_INCLUDE_DIRS})
include_directories(${Xext_INCLUDE_DIRS})
include_directories(${BOOST_INCLUDE_DIRS})
include_directories(${JPEG_INCLUDE_DIR})

set(BASE_PMVS base_pmvs)
set(PMVS pmvs2)
set(GENOPTION genOption)

set(PMVS_LIBRARIES ${Xext_LIBRARIES} ${X11_LIBRARIES} ${JPEG_LIBRARIES} ${LAPACK_LIBRARIES})

# PMVS

cs_add_library(${BASE_PMVS}	src/pmvs/detectFeatures.cc
							src/pmvs/detector.cc
							src/pmvs/dog.cc
							src/pmvs/expand.cc
							src/pmvs/filter.cc
							src/pmvs/findMatch.cc
							src/pmvs/harris.cc
							src/pmvs/image/camera.cc
							src/pmvs/image/image.cc
							src/pmvs/image/photo.cc
							src/pmvs/image/photoSetS.cc
							src/pmvs/numeric/mylapack.cc
							src/pmvs/optim.cc
							src/pmvs/option.cc
							src/pmvs/patch.cc
							src/pmvs/patchOrganizerS.cc
							src/pmvs/point.cc
							src/pmvs/seed.cc)


target_link_libraries(${BASE_PMVS} ${PMVS_LIBRARIES})

cs_add_executable(${PMVS} src/pmvs2.cc)
target_link_libraries(${PMVS} ${BASE_PMVS})

# GENOPTION

cs_add_executable(${GENOPTION} src/genOption.cc)

cs_install()
cs_export()