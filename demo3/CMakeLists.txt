cmake_minimum_required(VERSION 3.4)

PROJECT(HELLOLIB)
# 添加头文件的查找路径
include_directories(${PROJECT_SOURCE_DIR}/include)

#设置动态库的生成路径
SET(LIBRARY_OUTPUT_PATH ${PROJECT_SOURCE_DIR}/lib)
SET(LIBHELLO_SRC src/hello.cpp)
ADD_LIBRARY(hello SHARED ${LIBHELLO_SRC})

# 动态库版本号设置, VERSION 指代动态库版本，SOVERSION 指代 API 版本。
SET_TARGET_PROPERTIES(hello PROPERTIES VERSION 1.2 SOVERSION 1)

# 同一个cmake中不可以同时 用ADD_LIBRARY来生成两个同名的静态库和动态库,所以下面的语句应该被注释掉,可以修改静态库的名字,来同时生成静态库和动态库
# 例如使用下面的语句: ADD_LIBRARY(hello_static STATIC ${LIBHELLO_SRC}),但是这种不是我们想要的
#ADD_LIBRARY(hello STATIC ${LIBHELLO_SRC})
#ADD_LIBRARY(hello_static STATIC ${LIBHELLO_SRC})

SET_TARGET_PROPERTIES(hello PROPERTIES CLEAN_DIRECT_OUTPUT 1)
# 用下面的语句来生成静态库
ADD_LIBRARY(hello_static STATIC ${LIBHELLO_SRC})
SET_TARGET_PROPERTIES(hello_static PROPERTIES OUTPUT_NAME "hello")

#安装共享库和头文件
INSTALL(TARGETS hello hello_static
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)
INSTALL(FILES include/hello.h DESTINATION include/hello)