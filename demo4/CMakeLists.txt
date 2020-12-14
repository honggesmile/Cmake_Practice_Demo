cmake_minimum_required(VERSION 3.4)

project(demo4)

# include_directories添加头文件的搜索路径
include_directories(/usr/local/include/hello)

add_executable(main src/main.cpp)
message(STATUS "CMAKE_SYSTEM_PROCESSOR: " ${CMAKE_SYSTEM_NAME})
IF(CMAKE_SYSTEM_NAME STREQUAL "Linux")
    message("linux")
ELSE()
    message("not linux")
endif()

# 添加库的查找路径
link_directories("/usr/local/lib/")
#链接
target_link_libraries(main /usr/local/lib/libhello.so)
#target_link_libraries(main hello)

#EXEC_PROGRAM(ls ARGS "*.c" OUTPUT_VARIABLE LS_OUTPUT RETURN_VALUE LS_RVALUE)
#IF(not LS_RVALUE)
#    MESSAGE(STATUS "ls result: " ${LS_OUTPUT})
#ENDIF(not LS_RVALUE)
FIND_LIBRARY(libX X11 /usr/lib)
IF(NOT libX)
    MESSAGE(FATAL_ERROR "libX not found")
ELSE()
    MESSAGE("find libx")
ENDIF(NOT libX)

IF(WIN32)
    MESSAGE(STATUS "This is windows.")
    #作一些 Windows 相关的操作
ELSE(WIN32)
    MESSAGE(STATUS "This is not windows")
    #作一些非 Windows 相关的操作
ENDIF(WIN32)

AUX_SOURCE_DIRECTORY(build SRC_LIST)
FOREACH(F ${SRC_LIST})
    MESSAGE(${F})
ENDFOREACH(F)