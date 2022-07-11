cmake_minimum_required(VERSION 3.8)

project(mingw-mlpack-issue-20220708 LANGUAGES C CXX)

enable_testing()

find_package(OpenMP)
find_package(MLPACK REQUIRED)

# HACK: the absolute path to the libraries is hardcoded
# in the .pc and .cmake import target file, which is not
# portable. Here, we replace the hardcoded prefix using
# the MinGW root obtained with cygpath.
execute_process(
    COMMAND cygpath.exe -a -m /mingw64
    OUTPUT_VARIABLE MINGW_ROOT
    OUTPUT_STRIP_TRAILING_WHITESPACE
)
message("MINGW_ROOT=${MINGW_ROOT}")

get_target_property(TMP mlpack::mlpack INTERFACE_LINK_LIBRARIES)
string(REPLACE "D:/a/msys64/mingw64" "${MINGW_ROOT}" TMP_FIX "${TMP}")
set_target_properties(mlpack::mlpack PROPERTIES INTERFACE_LINK_LIBRARIES ${TMP_FIX})
message("BEFORE: ${TMP}")
message("AFTER : ${TMP_FIX}")

add_executable(test_mlpack main.cpp)

target_link_libraries(test_mlpack PRIVATE OpenMP::OpenMP_CXX mlpack::mlpack)

add_test(NAME test_mlpack COMMAND test_mlpack)
