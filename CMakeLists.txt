cmake_minimum_required(VERSION 3.8)

project(mingw-mlpack-issue-20220708 LANGUAGES C CXX)

enable_testing()

find_package(OpenMP)
option(USE_PKG_CONFIG "Use pkg-config to find mlpack" ON)
set(LIB_LST)

if (USE_PKG_CONFIG)
    find_package(PkgConfig REQUIRED)
    pkg_search_module(MLPACK_PKG REQUIRED IMPORTED_TARGET mlpack)
    set(LIB_LST PkgConfig::MLPACK_PKG)
else()
    find_package(MLPACK REQUIRED)
    set(LIB_LST mlpack::mlpack)
endif()

add_executable(test_mlpack main.cpp)

target_link_libraries(test_mlpack PRIVATE OpenMP::OpenMP_CXX ${LIB_LST})

add_test(NAME test_mlpack COMMAND test_mlpack)
