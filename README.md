# CMakePublic
A repository containing a very simple C++ library. The main purposes of this 
repo are:

- showcase what a well written, modern CMake build system looks like
- have a public GitHub-based, C++ library with a CMake build system for unit 
  testing CMaize
- the resulting library creates a function `call_cmake_public` which always
  returns 3 (*i.e.*, it's not very useful for actual C++ purposes...)  

## Installing CMakePublic

CMakePublic is installed via the usual CMake workflow:

```.bash
# Obtain the source code (skip if you've already done this)
git clone https://github.com/CMaizeExamples/CMakePublic.git
cd CMakePublic

# Configure
cmake -H. -B<build_dir> -DCMAKE_INSTALL_PREFIX=<where/to/install>

# Build
cmake --build <build_dir>

# Install
cmake --build <build_dir> -- target install
```

where:

- `<build_dir>` is the name of a directory where the build files will be stored.
- `<where/to/install>` is the name of the directory where the finished library
  should be installed to.
  - If you do not specify this CMake will default to the operating system 
    specific path for user-wide software.
    - You really do not want this library installed user-wide...

After installing `<where/to/install>` should minimally contain:

- The actual library `lib/libCMakePublic.a`
  - The extension and name will vary from operating system to operating system
- The header file `include/cmake_public.hpp`
- The CMake packaging files:
  - `lib/cmake/CMakePublicConfig.cmake`

Additional files (such a build type specific config file) may also be present
depending on the exact configuration command you (or your IDE) use.