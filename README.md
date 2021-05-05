# Library for Efficient Large-Scale Stereo Matching (ELAS) with OpenCV support

This is a port of the [libelas](http://www.cvlibs.net/software/libelas/) (LIBrary for Efficient LArge-scale Stereo matching) C++ library for stereo matching to work with [OpenCV](https://opencv.org/) and support the [meson](https://mesonbuild.com/) build system additionally to CMake.
The library implements a stereo matching method proposed in the following publication:

```
@INPROCEEDINGS{Geiger10,
 author = {Andreas Geiger and Martin Roser and Raquel Urtasun},
 title = {Efficient Large-Scale Stereo Matching},
 booktitle = {Asian Conference on Computer Vision},
 year = {2010},
 month = {November},
 address = {Queenstown, New Zealand}
}
```

If you use this library, please cite the above paper.

## Differences

- The CMakeLists.txt was adapted to include the OpenCV dependency and to build a library target. Further, the example file is excluded from the default build targets and needs to be build explicitly. Additionally, compile flags for Visual Studio were added.
- Meson build support was added (meson.build and meson_options.txt file).
- The PROFILE flag was added to both build systems as command line argument so that it can be switched on and off without changing anything in the code.
- Include files were moved to own include directory.
- Two functions to convert images from and to OpenCV matrices (imageFromCvMat and cvMatFromImage) were implemented in image.h to add support for OpenCV.
- The elas namespace was added to elas.h, elas.cpp and image.h.
- Compile warnings in all files were handled (see comments in header of files) and Visual Studio specific defines for fixed-width data types were removed since they are not required anymore.
- Matlab support was removed.

## Building 

### Prerequisites

- C++ compiler
- [meson](https://mesonbuild.com/) or [CMake](http://www.cmake.org/)
- [ninja](https://ninja-build.org/) or [make](https://en.wikipedia.org/wiki/Make_(software))
- [OpenCV](https://opencv.org/) C++ library

### Build Instructions

- Move to project root directory

#### Meson

- Run meson to initialize build directory: `meson build`
- Build library and example with ninja: `ninja -C build`

#### CMake

- Create build directory and enter it: `mkdir build && cd build`
- Run cmake: `cmake .. && cd ../`
- Build library: `make -C build`
- Build example: `make -C build example`

#### Compile Options

- With the `elas_profiler` build flag, the runtime measurement of the elas library can be activated.

### Run example

- Run './build/example demo' => computes disparity maps for images from the **img** directory.

