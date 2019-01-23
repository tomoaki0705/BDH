# minimum requirement
cmake_minimum_required(VERSION 3.6)

SET(SOLUTION_NAME BDH_ICCV_2013)

# Find OpenCV
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

# build main library
set(BDH_PATH ${CMAKE_SOURCE_DIR}/BDH/src)
set(BDH_LIBRARY_SOURCE ${BDH_PATH}/BDH.cpp
                       ${BDH_PATH}/BDHtraining.cpp
                       ${BDH_PATH}/HashTable.cpp
                       ${BDH_PATH}/Subspace.cpp
                       ${BDH_PATH}/baseset.h
                       ${BDH_PATH}/BDH.h
                       ${BDH_PATH}/BDHtraining.h
                       ${BDH_PATH}/define.h
                       ${BDH_PATH}/HashTable.h
                       ${BDH_PATH}/k_means.h
                       ${BDH_PATH}/NearestNeighbor.h
                       ${BDH_PATH}/point.h
                       ${BDH_PATH}/Subspace.h)

if(MSVC)
    add_definitions("/wd4265 /wd4266 /wd4350 /wd4365 /wd4435 /wd4514 /wd4625 /wd4626 /wd4640 /wd4668 /wd4710 /wd4819 /wd4820 /wd4946")
endif(MSVC)

add_library(${BDH_LIBRARY} STATIC ${BDH_LIBRARY_SOURCE})
target_link_libraries(${BDH_LIBRARY_SOURCE} ${OpenCV_LIBS})

# set TARGET_NAME as start up property
set_property(DIRECTORY PROPERTY VS_STARTUP_PROJECT ${BDH_LIBRARY})

