cmake_minimum_required(VERSION 3.4)
PROJECT(HELLO)
ADD_SUBDIRECTORY(src bin)
#安装 COPYRIGHT/README
INSTALL(FILES COPYRIGHT README DESTINATION share/doc/cmake/t2)
#安装 runhello.sh，直接修改主工程文件 CMakeLists.txt，加入如下指令：
INSTALL(PROGRAMS runhello.sh DESTINATION bin)
#安装 doc 中的 hello.txt
INSTALL(DIRECTORY doc/ DESTINATION share/doc/cmake/t2)

