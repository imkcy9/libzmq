cmake_minimum_required(VERSION "2.8.1")           # CMake 最低版本要求，低于则构建过程会被终止。
PROJECT(demo)

include_directories("${ZeroMQ_SOURCE_DIR}/include")

AUX_SOURCE_DIRECTORY(./ SRC_LIST)
AUX_SOURCE_DIRECTORY(../public/src SRC_LIST)
AUX_SOURCE_DIRECTORY(../public/src/timer SRC_LIST)
SET(EXECUTABLE_OUTPUT_PATH ./bin)

SET(CMAKE_CXX_COMPILER g++)

#add_compile_options(-std=c++11)
#add_compile_options(-std=c++11)
#SET(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
ADD_DEFINITIONS(-std=c++11 -g -W -Wall -Wno-unused -DUSE_SPDLOG -DZMQ_BUILD_DRAFT_API -DSPDLOG_TRACE_ON -DLINUX -Werror=return-type -Werror=nonnull -Werror=invalid-offsetof -Wno-deprecated ${CMAKE_CXX_FLAGS})

INCLUDE_DIRECTORIES(
	./src/
	../public/include
        ../public/src/
	../public/src/timer
	../public/include/mysql-connector
	/usr/local/include
)

LINK_DIRECTORIES(
	/usr/local/lib
	../public/lib/ubuntu
	../../public/lib/ubuntu
)

ADD_EXECUTABLE(demo ${SRC_LIST} ys_decoder.cpp ys_decoder.h decoder_base.h zmq_ystech_msg_dispatcher.h)

TARGET_LINK_LIBRARIES(demo ${RT_LIBRARY} m libzmq pthread tinyxml2 dl)
