cmake_minimum_required(VERSION 3.10)
project(KAIST_ME553_Exercise1 LANGUAGES CXX)

find_package(raisim CONFIG REQUIRED)
find_package(Eigen3 REQUIRED)

include_directories (${EIGEN3_INCLUDE_DIRS})
file(COPY "${CMAKE_CURRENT_SOURCE_DIR}/rsc" DESTINATION ${CMAKE_BINARY_DIR})

function(create_executable app_name)
    add_executable(${app_name} src/${app_name}.cpp)
    if(NOT WIN32)
        target_link_libraries(${app_name} PUBLIC raisim::raisim pthread)
    else()
        target_link_libraries(${app_name} PUBLIC raisim::raisim Ws2_32)
    endif()
endfunction()

create_executable(demo_1)
create_executable(demo_2)
create_executable(exercise_1)