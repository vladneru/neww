cmake_minimum_required(VERSION 2.8.7)
project(${CMAKE_PROJECT_NAME}_test CXX)
set(Boost_USE_STATIC_LIBS ON)
set(Boost_USE_MULTITHREADED ON)
set(Boost_USE_STATIC_RUNTIME OFF)



file(GLOB SOURCES *.cpp)
add_executable(${PROJECT_NAME} ${SOURCES})
target_link_libraries(${PROJECT_NAME} ${Boost_LIBRARIES})
target_link_libraries(${PROJECT_NAME} ${OPENSSL_LIBRARIES} ${CURL_LIBRARY})

add_test(NAME ${PROJECT_NAME} COMMAND ${PROJECT_NAME} "-s" "-r" "compact" "--use-colour" "yes")
