cmake_minimum_required(VERSION 3.0.0)
project(hello_laser VERSION 0.1.0)

#Inlcude wjwwood serial include files
include_directories(wjwwood-serial/include)
enable_testing()

if(APPLE)
    find_library(IOKIT_LIBRARY IOKit)
    find_library(FOUNDATION_LIBRARY Foundation)
endif()

if(UNIX AND NOT APPLE)
    # If Linux, add rt and pthread
    set(rt_LIBRARIES rt)
    set(pthread_LIBRARIES pthread)
endif()

## Define the sources and locations of the wjwwood-serial library
## They differ depending on OS
set(serial_SRCS
    wjwwood-serial/src/serial.cc
    wjwwood-serial/include/serial/serial.h
    wjwwood-serial/include/serial/v8stdint.h
)

if(APPLE)
    # If OSX
    list(APPEND serial_SRCS  wjwwood-serial/src/impl/unix.cc)
    list(APPEND serial_SRCS  wjwwood-serial/src/impl/list_ports/list_ports_osx.cc)
elseif(UNIX)
    # If unix
    list(APPEND serial_SRCS  wjwwood-serial/src/impl/unix.cc)
    list(APPEND serial_SRCS  wjwwood-serial/src/impl/list_ports/list_ports_linux.cc)
else()
    # If windows
    list(APPEND serial_SRCS  wjwwood-serial/src/impl/win.cc)
    list(APPEND serial_SRCS  wjwwood-serial/src/impl/list_ports/list_ports_win.cc)
endif()

add_library(wjwwood-serial ${serial_SRCS})

## Link to the appropriate library containing OS serial port driver
if(APPLE)
    target_link_libraries(wjwwood-serial ${FOUNDATION_LIBRARY} ${IOKIT_LIBRARY})
elseif(UNIX)
    target_link_libraries(wjwwood-serial rt pthread)
else()
    target_link_libraries(wjwwood-serial setupapi)
endif()

# Add the executable file
add_executable(${PROJECT_NAME} main.cpp)

# Add the wjwood-serial dependancy and link it to our exe
add_dependencies(${PROJECT_NAME} wjwwood-serial)
target_link_libraries(${PROJECT_NAME} wjwwood-serial)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})
include(CPack)
