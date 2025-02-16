# -DCMAKE_BUILD_TYPE=Debug
CMAKE_MINIMUM_REQUIRED(VERSION 2.6)
project( uniform_sampling_pointcloud )

SET(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${PROJECT_SOURCE_DIR}/CMakeModules/")

set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS}  -O3")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -O3")

# Overide with cmake -DCMAKE_BUILD_TYPE=Debug {dir}
IF( NOT CMAKE_BUILD_TYPE )
   SET( CMAKE_BUILD_TYPE Release )
ENDIF()

# Platform configuration vars
#INCLUDE(SetPlatformVars)

FIND_PACKAGE(CUDA REQUIRED)
FIND_PACKAGE(GLEW REQUIRED)
FIND_PACKAGE(VTK REQUIRED)
FIND_PACKAGE(Pangolin REQUIRED)
FIND_PACKAGE(freenect REQUIRED)
FIND_PACKAGE(freenectsync REQUIRED)
FIND_PACKAGE(Cg REQUIRED)
#FIND_PACKAGE(MinimalImgUtilities REQUIRED)
FIND_PACKAGE(OpenMP REQUIRED)
FIND_PACKAGE(G2O REQUIRED)
FIND_PACKAGE(ASSIMP REQUIRED)
FIND_PACKAGE(Sophus REQUIRED)
FIND_PACKAGE(Eigen3 REQUIRED)
FIND_PACKAGE(CSparse)
#FIND_PACKAGE(OpenNI2 REQUIRED)
FIND_PACKAGE(CVD REQUIRED)
FIND_PACKAGE(Cg REQUIRED)
FIND_PACKAGE(PCL REQUIRED)
FIND_PACKAGE(osg REQUIRED)
FIND_PACKAGE(ZLIB REQUIRED)



SET(
  SOURCES
)


INCLUDE_DIRECTORIES(
        ${CMAKE_CURRENT_SOURCE_DIR}
        ${CMAKE_SOURCE_DIR}
        ${CMAKE_CURRENT_BINARY_DIR}
)

INCLUDE_DIRECTORIES(
  ${ASSIMP_INCLUDE_DIR}
  ${CUDA_CUT_INCLUDE_DIR}
  ${CUDA_INCLUDE_DIRS}
  ${VTK_INCLUDE_DIRS}
  ${freenect_INCLUDE_DIR}
  ${freenectsync_INCLUDE_DIR}
  ${OpenNI2_INCLUDE_DIR}
  ${OpenCV2_INCLUDE_PATH}
  ${Pangolin_INCLUDE_DIR}
  ${CG_INCLUDE_PATH}
  ${MinimalImgUtilities_INCLUDE_DIR}
  ${ICARUS_INCLUDE_DIR}
  ${EIGEN3_INCLUDE_DIR}
  ${G2O_INCLUDE_DIR}
  ${CSPARSE_INCLUDE_DIR}
  ${CVD_INCLUDE_DIR}
  ${PCL_INCLUDE_DIRS}
  ${OPENCV_INCLUDE_DIRS}
  ${OSG_INCLUDE_DIRS}
  ${ZLIB_INCLUDE_DIR}
  /usr/include/ni
  /usr/lib/x86_64-linux-gnu/glib-2.0/include
  /usr/include/glib-2.0
  /usr/lib/glib-2.0/include
)

LINK_DIRECTORIES(
  ${OPENCV_LIBRARY_DIRS}
  ${CUDA_SDK_ROOT_DIR}/lib
  ${CUDA_SDK_ROOT_DIR}/common/lib
  /usr/local/lib
  /usr/local/lib64/osgPlugins-3.3.3
  /usr/local/lib64
)

message("PCL LIBRARY = " ${PCL_LIBRARIES})
message("PCL INCLUDE LIBRARY = " ${PCL_INCLUDE_DIRS})
#message("VTK INCLUDE DIRS = ${VTK_INCLUDE_DIRS}")
message("Cg INCLUDE DIRS = ${CG_INCLUDE_PATH}")
message("OSG_INCLUDE_DIRS = ${OSG_INCLUDE_DIRS}")
message("OSG_FOUND = ${OSG_LIBRARY}")


LINK_LIBRARIES(
  ${ASSIMP_LIBRARY}
  ${LIBRARY_NAME}
  ${Pangolin_LIBRARY}
  ${VTK_LIBRARIES}
  ${freenect_LIBRARY}
  ${OpenNI2_LIBRARY}
  ${freenectsync_LIBRARY}
  ${CG_LIBRARY}
  ${CG_GL_LIBRARY}
  ${MinimalImgUtilities_LIBRARY}
  ${ICARUS_LIBRARY}
  ${Eigen3_LIBRARY}
  ${G2O_STUFF_LIBRARY}
  ${G2O_CORE_LIBRARY}
  ${G2O_SOLVER_CSPARSE}
  ${G2O_SOLVER_CSPARSE_EXTENSION}
  ${CSPARSE_LIBRARY}
  ${CVD_LIBRARY}
  ${PCL_LIBRARIES}
  ${OpenCV_LIBS}
  ${OSG_LIBRARY}
  ${ZLIB_LIBRARIES}
  -lOpenNI
  -lGLEW
  -lglut
  -lGLU
  -lcutil_x86_64
  -lGL
  -lgts
  -lglib-2.0
  -lboost_system
  -lpcl_search
  -lboost_filesystem
  -lboost_thread
  -lblas
  -llapack
  -lcholmod
  -lboost_timer
#  -lpthread
   /usr/local/lib64/osgPlugins-3.3.3/osgdb_obj.so
   /usr/local/lib64/libosgDB.so
   -losg
   /usr/local/lib64/libosgViewer.so
   /usr/local/lib64/libosgManipulator.so
   /usr/local/lib64/libosgGA.so
  -lGVars3
   /usr/lib/x86_64-linux-gnu/libopencv_core.so
   /usr/lib/x86_64-linux-gnu/libopencv_features2d.so
)

message("PCL LIBRARY = " ${PCL_LIBRARIES})
message("PCL INCLUDE LIBRARY = " ${PCL_INCLUDE_DIRS})

LINK_LIBRARIES(
  ${PCL_LIBRARIES}
  ${Eigen3_LIBRARY}
  ${CSPARSE_LIBRARY}
  -lpcl_search
  -lcholmod
)

IF(OPENMP_FOUND)
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS} ${OpenMP_EXE_LINKER_FLAGS}")
ENDIF()

ADD_EXECUTABLE(deformable_lc
               ./src/main_deformable_lc.cpp)

ADD_EXECUTABLE(drifting_reconstruction
               ./src/main_iclnuim_drift_recon.cpp)
