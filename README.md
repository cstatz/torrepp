# torrepp

### Status

[![Build Status](https://github.com/cstatz/torrepp/workflows/cmake-linux/badge.svg)](https://github.com/cstatz/torrepp/actions) 
[![License](https://img.shields.io/badge/License-BSD%203-brightgreen)](https://opensource.org/licenses/BSD-3-Clause)

## Content

1. [Introduction](#introduction)
    1. [Contributing](#contributing)
    2. [Versions](#versions)
2. [Features](#features)
3. [Installation](#installation)
    1. [Dependencies](#dependencies)
    2. [Clone the repository](#clone-the-repository)
    3. [Build and Test](#build-and-test)
    4. [Configuration](#configuration)
4. [Usage](#usage)
    1. [Examples](#examples)
    2. [Minimal Examples](#minimal-example)
    3. [Notes](#notes)
5. [Benchmarks](#benchmarks)
6. [License](#license)


## Introduction

### Contributing
We appreciate all contributions from issues to pull requests. 

For contributing, please read the [contribution guide](CONTRIBUTING.md).

### Versions
The releases are based on the master branch. The release-version is tagged and follows the scheme Year.Quarter.Revision.

## Features
- [x] modern C++
- [x] unit tests via [doctest](https://github.com/onqtam/doctest)

## Installation
Installation and build are tested on linux (e.g. ubuntu bionic, arch linux) and macOS.
Before starting the build process please ensure all dependencies are properly installed and available to the project.

### Dependencies
 * C++17 capable compiler
 * cmake (>= 3.11.0)
 * [doctest](https://github.com/onqtam/doctest) (for testing, pulled in as submodule)

### Clone the repository

Clone the repository with the following command:
```git clone https://github.com/cstatz/torrepp.git```

For the tests and the benchmarks the submodules must be cloned as well:
```
git submodule init
git submodule update 
```
This will pull doctest, ... as submodules.

### Build and test

We strictly recommend an out-of-source build in a separate directory (here for simplicity ```build```) 
Starting in the source directory to project is build from the commandline as follows:
```shell script
mkdir build
cd build 
ccmake ../  # create cache and configuration
cmake --build .
cmake --build . -- install  # If package needs to be installed 
ctest  # Runs the tests
```

**For maximum performance**, we recommend building with **gcc** which results in a 15% to 20% better performance
compared to clang (on linux and macOS). The provided benchmarks might be used to tune the compilation flags for your 
specific system and architecture.


### Configuration
The easiest way to set the configuration variables is by using ```ccmake``` or pass the variables
via ```cmake ../ -D<VARIABLE>:<TYPE>=value```.

- ```ENABLE_OMP```: Enable OpenMP in examples (for traversal)
- ```BUILD_TEST```: Build tests

## Usage

### Examples

### Minimal Example

### Notes

## Benchmarks

## License

torrepp is licensed under the new **BSD (3-clause) license**.
[cnpy](https://github.com/rogersce/cnpy) is licensed under the MIT license and available at: https://github.com/rogersce/cnpy
