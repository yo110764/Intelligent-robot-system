#  minimum required cmake version: 3.1.0
cmake_minimum_required(VERSION 3.1.0)

project(RealsenseExamplesSoftwareDevice)

# Save the command line compile commands in the build output
set(CMAKE_EXPORT_COMPILE_COMMANDS 1)

include(CheckCXXCompilerFlag)
CHECK_CXX_COMPILER_FLAG("-std=c++11" COMPILER_SUPPORTS_CXX11)
CHECK_CXX_COMPILER_FLAG("-std=c++0x" COMPILER_SUPPORTS_CXX0X)
if(COMPILER_SUPPORTS_CXX11)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")
elseif(COMPILER_SUPPORTS_CXX0X)
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++0x")
endif()

if(BUILD_GRAPHICAL_EXAMPLES)
    add_executable(rs-software-device rs-software-device.cpp)
    target_link_libraries(rs-software-device ${DEPENDENCIES})
    include_directories(rs-software-device ../ ../../third-party/tclap/include ../../third-party/ ../../common/res)
    set_target_properties (rs-software-device PROPERTIES
        FOLDER "Examples"
    )

    install(
        TARGETS

        rs-software-device

        RUNTIME DESTINATION
        ${CMAKE_INSTALL_PREFIX}/bin
    )
endif()
