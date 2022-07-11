# mingw-mlpack-issue-20220708
Small snippet to reproduce the runtime error issue related to missing symbol in libarmadillo.dll.

```
# install dependency
pacman -S mingw-w64-x86_64-mlpack

# configure and compile

cmake -G Ninja .
cmake --build .
strace ./test_mlpack.exe
```

