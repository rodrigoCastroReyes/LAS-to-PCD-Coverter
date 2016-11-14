cmake_minimum_required(VERSION 2.6 FATAL_ERROR)
project(pcl_reader)
find_package(PCL 1.3 REQUIRED COMPONENTS common io)


SET(LAS_LIB_DIR /home/rodrigo/Descargas/LAStools/LASlib/lib)
SET(LAS_LIB_INCLUDE /home/rodrigo/Descargas/LAStools/LASlib/inc)
SET(LAS_LIB_SRC /home/rodrigo/Descargas/LAStools/LASzip/src)

add_library(liblas STATIC IMPORTED)
set_target_properties(liblas PROPERTIES IMPORTED_LOCATION ${LAS_LIB_DIR}/liblas.a)

include_directories(${LAS_LIB_INCLUDE} ${LAS_LIB_SRC} ${PCL_INCLUDE_DIRS} )
link_directories(${LAS_LIB_SRC} ${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})

add_executable(las_to_pcd las_to_pcd.cpp)
target_link_libraries(las_to_pcd ${PCL_COMMON_LIBRARIES} ${PCL_IO_LIBRARIES} ${LAS_LIB_DIR}/liblas.a)