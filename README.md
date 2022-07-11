# mingw-mlpack-issue-20220708
Small snippet to reproduce the runtime error issue related to missing symbol in libarmadillo.dll.

```
# install dependency
pacman -S mingw-w64-x86_64-mlpack

# configure and compile

cmake -G Ninja .
cmake --build .
strace ./test_mlpack.exe
# Entry Point Not Found
# The procedure entry point _ZN4arma15H5check_versionEjjj could not be located in the dynamic link library libmlpack.dll

# Expected output:
$ ./test_mlpack.exe
Nearest neighbor of point 0 is point 3 and the distance is 0.449757.
Nearest neighbor of point 1 is point 2 and the distance is 0.918409.
Nearest neighbor of point 2 is point 1 and the distance is 0.918409.
Nearest neighbor of point 3 is point 0 and the distance is 0.449757.

```

