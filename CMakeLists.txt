cmake_minimum_required(VERSION 2.8)
project(icp_analysis)

set(CMAKE_MODULE_PATH ${PROJECT_SOURCE_DIR}/cmake ${CMAKE_MODULE_PATH})
set(CMAKE_CXX_FLAGS "-std=c++14 ${CMAKE_CXX_FLAGS}")
add_definitions(-DPROJECT_DIR="${PROJECT_SOURCE_DIR}")

# Eigen
find_package(Eigen3 REQUIRED)
include_directories(${EIGEN3_INCLUDE_DIR})

# FreeImage
find_package(FreeImage REQUIRED)
include_directories(${FREEIMAGE_INCLUDE_DIRS})

# Flann
find_package(Flann REQUIRED)
include_directories(${FLANN_INCLUDE_DIRS})

# Ceres Solver
find_package(Ceres REQUIRED)
include_directories(${CERES_INCLUDE_DIRS})

# Set files to be compiled
set(HEADER_FILES 
    Eigen.h 
    SimpleMesh.h 
    PointCloud.h 
    VirtualSensor.h 
    NearestNeighbor.h 
    ProcrustesAligner.h 
    ICPOptimizer.h 
    FreeImageHelper.h
)
set(SOURCE_FILES 
    FreeImageHelper.cpp
)

add_executable(icp_analysis main.cpp ${HEADER_FILES} ${SOURCE_FILES})
target_link_libraries(icp_analysis ${FREEIMAGE_LIBRARIES} ${FLANN_LIBRARIES} ${CERES_LIBRARIES})
