project(objc.A.dylib)

cmake_minimum_required(VERSION 2.4.0)
if(COMMAND cmake_policy)
	cmake_policy(SET CMP0003 NEW)
endif(COMMAND cmake_policy)

enable_language(ASM_NASM)

#if (NOT "${CMAKE_CXX_COMPILER} ${CMAKE_CXX_COMPILER_ARG1}" MATCHES ".*clang")
#	message(FATAL_ERROR "Clang is the only supported compiler.")
#endif (NOT "${CMAKE_CXX_COMPILER} ${CMAKE_CXX_COMPILER_ARG1}" MATCHES ".*clang")

#configure_file(config.h.in config.h)
#set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -fblocks -std=c++0x")
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -std=c99")

set(objcdarwin_SRCS
	objc_msgSend.nasm
	objc_msgSend_fixup.nasm
	dummy.c
)

add_library(objc.A.dylib SHARED ${objcdarwin_SRCS})
target_link_libraries(objc.A.dylib -l:libobjc.so.4)

install(TARGETS objc.A.dylib DESTINATION lib${SUFFIX})
