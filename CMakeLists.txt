cmake_minimum_required(VERSION 3.8)

project(curl)

set(CMAKE_VERBOSE_MAKEFILE ON)

set(CDEFFINE_FLAGS "-DHAVE_CONFIG_H -DBUILDING_LIBCURL -DHTTP_ONLY")
set(CMAKE_C_FLAGS "${CMAKE_CXX_FLAGS} ${CDEFFINE_FLAGS} -fPIC" )

FILE(GLOB SOURCES
        lib/*.c
        lib/*/*.c
        )
add_library(${PROJECT_NAME} STATIC ${SOURCES} )
add_library(vendor::${PROJECT_NAME} ALIAS ${PROJECT_NAME})

target_include_directories(${PROJECT_NAME}
        PUBLIC
        ${PROJECT_SOURCE_DIR}/include
        ${PROJECT_SOURCE_DIR}/lib
        ${PROJECT_SOURCE_DIR}/lib/vtls
	${OPENSSL_ROOT_DIR}/include
        )



