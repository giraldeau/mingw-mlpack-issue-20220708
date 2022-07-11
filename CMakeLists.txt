cmake_minimum_required(VERSION 3.8)

project(ats-ml LANGUAGES C CXX)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${CMAKE_SOURCE_DIR}/cmake")

enable_testing()

find_package(OpenMP)
#find_package(Boost REQUIRED COMPONENTS serialization program_options unit_test_framework)

find_package(MLPACK REQUIRED)
find_package(Armadillo REQUIRED)

add_executable(test_mlpack main.cpp)

target_include_directories(test_mlpack PRIVATE
    ${ARMADILLO_INCLUDE_DIRS}
    ${MLPACK_INCLUDE_DIRS}
)

target_link_libraries(test_mlpack
    OpenMP::OpenMP_CXX
    ${ARMADILLO_LIBRARIES}
    ${MLPACK_LIBRARIES}
)

add_test(NAME test_mlpack COMMAND test_mlpack)