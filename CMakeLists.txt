cmake_minimum_required(VERSION 3.6)

# Project Name (and also the compiled binary's name)
project(libsoundiopp)
set(CMAKE_BUILD_TYPE Release)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY "./lib")

# Flags to send to the compiler
# OBS: Do NOT use Linker OR Include flags (CMAKE take care of this for you)
set(CMAKE_CXX_FLAGS
        "${CMAKE_CXX_FLAGS} -std=c++11 -O3"
)

# List of Header files (.h, .hh, .hpp)
set(HEADER_FILES
        include/soundiopp/enums.h
        include/soundiopp/soundiopp.h
)

# List of Source files (.c, .cc, .cpp)
set(SOURCE_FILES
        src/channellayout.cpp
        src/context.cpp
        src/device.cpp
        src/instream.cpp
        src/outstream.cpp
        src/ringbuffer.cpp
        src/soundiopp.cpp
        src/templates.h
)

# Include Projet cmake scripts (Mostly used to find dependencies libraries on the system)
set(CMAKE_MODULE_PATH
        ${CMAKE_MODULE_PATH}
        ${CMAKE_SOURCE_DIR}/cmake
)

# Execute each dependency find_cmake script
find_package(SoundIo REQUIRED)

# Specify which project's files will be compiled
add_library(${PROJECT_NAME} SHARED
        ${HEADER_FILES}
        ${SOURCE_FILES}
)

# Include the dependencies header files to be compiled
include_directories(
        ${SOUNDIO_INCLUDE_DIR}
)

# Link the dependencies libs
target_link_libraries(
        ${PROJECT_NAME}
        ${SOUNDIO_LIBRARY}
)