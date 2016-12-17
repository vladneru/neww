cmake_minimum_required(VERSION 2.8.7)
project(catch_builder CXX)
include(ExternalProject)
find_package(Git REQUIRED)

ExternalProject_Add(
    catch
    PREFIX ${CMAKE_BINARY_DIR}/catch
    GIT_REPOSITORY https://github.com/philsquared/Catch.git
    TIMEOUT 10
    UPDATE_COMMAND ${GIT_EXECUTABLE} pull
    CONFIGURE_COMMAND ""
    BUILD_COMMAND ""
    INSTALL_COMMAND ""
    LOG_DOWNLOAD ON
)


ExternalProject_Get_Property(catch source_dir)
set(CATCH_INCLUDE_DIR ${source_dir}/include CACHE INTERNAL "Path to include folder for Catch")
PROJECT(${GLOBAL_PROJECT_NAME})
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14 -fdiagnostics-color=always")
include_directories("include")

set(Boost_USE_STATIC_LIBS ON)
set(Boost_USE_MULTITHREADED ON)
set(Boost_USE_STATIC_RUNTIME OFF)

find_package(OpenSSL REQUIRED)
find_package(Boost REQUIRED)
find_package(CURL REQUIRED)
include_directories(${CURL_INCLUDE_DIR})

include_directories(${Boost_INCLUDE_DIRS})
target_link_libraries(neww ${Boost_LIBRARIES})

add_subdirectory(sources)
include_directories(${CATCH_INCLUDE_DIR})
enable_testing(true)
add_subdirectory(tests)
