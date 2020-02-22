cmake_minimum_required(VERSION 3.15)
project(rxterm)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -ggdb -O3 -Wall")
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -ggdb -O3 -Wall")

find_package(Boost 1.53.0 REQUIRED COMPONENTS program_options)

file(GLOB RXTERM_SRC ${PROJECT_SOURCE_DIR}/rxterm/apps/*.cpp)

add_subdirectory(rxterm)
add_executable(rxterm.exe ${RXTERM_SRC})
target_include_directories(rxterm.exe PUBLIC ${PROJECT_SOURCE_DIR}/rxterm/include)
target_link_libraries(rxterm.exe rxterm)

if(Boost_FOUND)
    target_include_directories(rxterm.exe PUBLIC ${Boost_INCLUDE_DIRS})
    target_link_libraries(rxterm.exe ${Boost_LIBRARIES})
endif()
