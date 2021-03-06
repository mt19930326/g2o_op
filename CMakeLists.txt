cmake_minimum_required( VERSION 2.8 )
project( g2o_curve_fitting )

set( CMAKE_BUILD_TYPE "Release" )
set( CMAKE_CXX_FLAGS "-std=c++11 -O3" )

# 添加cmake模块以使用ceres库

list( APPEND CMAKE_MODULE_PATH /home/g2o/cmake_modules)
set(G2O_ROOT /home/g2o)
find_package(G2O REQUIRED)
include_directories(
${G2O_INCLUDE_DIRS}
"/usr/include/eigen3"
)
find_package( OpenCV REQUIRED )

# OpenCV
FIND_PACKAGE( CSparse )
INCLUDE_DIRECTORIES( ${G2O_INCLUDE_DIR} ${CSPARSE_INCLUDE_DIR} )
include_directories( ${OpenCV_DIRS} )

add_executable( curve_fitting main.cpp )
# 与G2O和OpenCV链接
target_link_libraries( curve_fitting 
    ${OpenCV_LIBS}
    g2o_core g2o_stuff
)
