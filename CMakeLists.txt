# minimum requirement
cmake_minimum_required(VERSION 3.6)

project(BDH_ICCV_2013)

# Find OpenCV
find_package(OpenCV REQUIRED)
include_directories(${OpenCV_INCLUDE_DIRS})

# build main library
set(BDH_LIBRARY BDH)
set(BDH_PATH ${CMAKE_SOURCE_DIR}/BDH/src)
set(BDH_INC_PATH ${CMAKE_SOURCE_DIR}/build/include)
set(BDH_LIBRARY_SOURCE ${BDH_PATH}/BDH.cpp
                       ${BDH_PATH}/BDHtraining.cpp
                       ${BDH_PATH}/HashTable.cpp
                       ${BDH_PATH}/Subspace.cpp
                       ${BDH_INC_PATH}/baseset.h
                       ${BDH_INC_PATH}/BDH.h
                       ${BDH_INC_PATH}/BDHtraining.h
                       ${BDH_INC_PATH}/define.h
                       ${BDH_INC_PATH}/HashTable.h
                       ${BDH_INC_PATH}/k_means.h
                       ${BDH_INC_PATH}/NearestNeighbor.h
                       ${BDH_INC_PATH}/point.h
                       ${BDH_INC_PATH}/Subspace.h)
include_directories(${BDH_INC_PATH})

set(DEMO demo)
set(UTILITY_PATH ${CMAKE_SOURCE_DIR}/testProjects/Utility)
set(UTILITY_SOURCE_PATH ${UTILITY_PATH}/src)
set(DEMO_SOURCES  ${CMAKE_SOURCE_DIR}/testProjects/demo/demoMain.cpp
                  ${UTILITY_SOURCE_PATH}/FileHandle.cpp
                  ${UTILITY_SOURCE_PATH}/measure.cpp
                  ${UTILITY_SOURCE_PATH}/superPCA.cpp
    )
include_directories(${UTILITY_PATH}/include ${CMAKE_SOURCE_DIR}/build/include ${OpenCV_INCLUDE_DIRS})

if(MSVC)
    add_definitions("/wd4265 /wd4266 /wd4350 /wd4365 /wd4435 /wd4514 /wd4625 /wd4626 /wd4640 /wd4668 /wd4710 /wd4819 /wd4820 /wd4946")
endif(MSVC)

add_library(${BDH_LIBRARY} STATIC ${BDH_LIBRARY_SOURCE})
add_executable(${DEMO} ${DEMO_SOURCES})

target_link_libraries(${DEMO} ${BDH_LIBRARY} ${OpenCV_LIBS})

# set TARGET_NAME as start up property
set_property(DIRECTORY PROPERTY VS_STARTUP_PROJECT ${BDH_LIBRARY})

