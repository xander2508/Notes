
[platform/superproject - Android Code Search](https://cs.android.com/android/platform/superproject)

## art

Contains the source code for the Android Runtime. Which is the managed runtime used for android applications.

Replaces Dalvik and provides ahead of time and just in time compilation time. Provides garbage collection.

Contains the compiler.

`art/compiler/Android.bp`= Blueprint file. How to build compiler, and related components in the art project. Defines the source files, deps, build target, flags to build the compiler

`art/compiler/cfi_test.h` = Contains the tests for the control flow integrity for the compiler. Ensures that the program control flow follows a legitimate path. Its job is to prevent control flow hijacking.

`art/compiler/compiler.cc` = Primary 