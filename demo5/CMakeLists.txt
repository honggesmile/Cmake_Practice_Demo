cmake_minimum_required(VERSION 3.4)

PROJECT(curl)
INCLUDE_DIRECTORIES(/usr/include)
ADD_EXECUTABLE(curltest src/main.cpp)
TARGET_LINK_LIBRARIES(curltest curl)
