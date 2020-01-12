# Chapter 01

## Standard predefined macro names

Quick reference: https://gcc.gnu.org/onlinedocs/cpp/Standard-Predefined-Macros.html

- `__FILE__`: The name of the current input file, in the form of a C string constant. This is the path by which the preprocessor opened the file, not the short name specified in `#include` or as the input file name argument.
- `__LINE__`: The current input line number, in the form of a decimal integer constant.
- `__DATE__`: A string constant that describes the date on which the preprocessor is being run, in the format of "Feb 12 1996". If the day of the month is less than 10, it is padded with a space on the left.
- `__TIME__`: A string constant that describes the time at which the preprocessor is being run, in the format of "23:59:01".
- ...

## GCC predefined macro names

To list gcc's predefined macros:

```
gcc -x c /dev/null -dM -E
```

### Checking OS

```
Linux and Linux-derived           __linux__
Android                           __ANDROID__ (implies __linux__)
Linux (non-Android)               __linux__ && !__ANDROID__
Darwin (Mac OS X and iOS)         __APPLE__
Akaros (http://akaros.org)        __ros__
Windows                           _WIN32
Windows 64 bit                    _WIN64 (implies _WIN32)
NaCL                              __native_client__
AsmJS                             __asmjs__
Fuschia                           __Fuchsia__
```

### Checking the compiler

```
Visual Studio       _MSC_VER
gcc                 __GNUC__
clang               __clang__
emscripten          __EMSCRIPTEN__ (for asm.js and webassembly)
MinGW 32            __MINGW32__
MinGW-w64 32bit     __MINGW32__
MinGW-w64 64bit     __MINGW64__
```

### Checking compiler version

```
// gcc
#if defined(__GNUC__) && (__GNUC___ > 5 || (__GNUC__ == 5 && __GNUC_MINOR__ >= 1))
// this is gcc 5.1 or greater
#endif

// clang
__clang_major__
__clang_minor__
__clang_pathchlevel__
```

### Checking processor arch

```
__i386__
__x86_64__
__arm__
__powerpc64__
__aarch64__
```

## Macro tricks

### Operators

* `#` turns the parameter into its string form surrounded by a pair of quotation marks.
* `##` concatenates the parameters to other elements in the macro definition and usually forms variable names.

### Variadic macros

`__VA_ARGS__` tells the preprocessor to replace it with all the remaining input arguments that are not assigned to any parameter yet.

```
#define LOG_ERROR(format, ...) fprintf(stderr, format, __VA_ARGS__)
```

