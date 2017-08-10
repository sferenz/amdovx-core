﻿# AMD OpenVX (AMDOVX)
AMD OpenVX (beta preview) is a highly optimized open source implementation of the [Khronos OpenVX](https://www.khronos.org/registry/vx/) computer vision specification. It allows for rapid prototyping as well as fast execution on a wide range of computer hardware, including small embedded x86 CPUs and large workstation discrete GPUs.

The amdovx-core project consists of two components:
* [OpenVX](openvx/README.md): AMD OpenVX library
* [RunVX](runvx/README.md): command-line utility to execute OpenVX graph described in GDF text file

The OpenVX framework provides a mechanism to add new vision functions to OpenVX by 3rd party vendors. Look into github [amdovx-modules](https://github.com/GPUOpen-ProfessionalCompute-Libraries/amdovx-modules) project for additional OpenVX modules and utilities.
* [vx_loomsl](https://github.com/GPUOpen-ProfessionalCompute-Libraries/amdovx-modules/tree/master/vx_loomsl/README.md): Radeon LOOM stitching library for live 360 degree video applications
* [loom_shell](https://github.com/GPUOpen-ProfessionalCompute-Libraries/amdovx-modules/tree/master/utils/loom_shell/README.md): an interpreter to prototype 360 degree video stitching applications using a script
* [vx_ext_cv](https://github.com/GPUOpen-ProfessionalCompute-Libraries/amdovx-modules/tree/master/vx_ext_cv/README.md): OpenVX module that implemented a mechanism to access OpenCV functionality as OpenVX kernels

This software is provided under a MIT-style license,  see the file COPYRIGHT.txt for details.

## Features
* The code is highly optimized for both x86 CPU and OpenCL for GPU
* Supported hardware spans the range from low power embedded APUs (like the new G series) to laptop, desktop and workstation graphics
* Supports Windows, Linux, and OS X
* Includes a “graph optimizer” that looks at the entire processing pipeline and removes/replaces/merges functions to improve performance and minimize bandwidth at runtime 
* Scripting support allows for rapid prototyping, without re-compiling at production performance levels

## Pre-requisites
* CPU: SSE4.1 or above CPU, 64-bit.
* GPU: Radeon R7 Series or above (Kaveri+ APU), Radeon 3xx Series or above (optional)
  * DRIVER: AMD Catalyst 15.7 or higher (version 15.20) with OpenCL 2.0 runtimes
  * AMD APP SDK 3.0 [download](http://developer.amd.com/tools-and-sdks/opencl-zone/amd-accelerated-parallel-processing-app-sdk/).

## Build Instructions
Build this project to generate AMD OpenVX library and RunVX executable. 
* Refer to [openvx/include/VX](openvx/include/VX) for Khronos OpenVX standard header files.
* Refer to [openvx/include/vx_ext_amd.h](openvx/include/vx_ext_amd.h) for vendor extensions in AMD OpenVX library.
* Refer to [runvx/README.md](runvx/README.md) for RunVX details. 

### Build using Visual Studio Professional 2013 on 64-bit Windows 10/8.1/7
* Install OpenCV 3 with contrib [download](https://github.com/opencv/opencv/releases) for RunVX tool to support camera capture and image display (optional)
* OpenCV_DIR environment variable should point to OpenCV/build folder
* Use amdovx-core/amdovx.sln to build for x64 platform
* If AMD GPU (or OpenCL 2.0) is not available, set build flag ENABLE_OPENCL=0 in openvx/openvx.vcxproj and runvx/runvx.vcxproj.

### Build using CMake
* Install CMake 2.8 or newer [download](http://cmake.org/download/).
* Install OpenCV 3 with contrib [download](https://github.com/opencv/opencv/releases) for RunVX tool to support camera capture and image display (optional)
* OpenCV_DIR environment variable should point to OpenCV/build folder
* Install libssl-dev on linux (optional)
* Use CMake to configure and generate Makefile
* If AMD GPU (or OpenCL 2.0) is not available, use build flag -DCMAKE_DISABLE_FIND_PACKAGE_OpenCL=TRUE.
