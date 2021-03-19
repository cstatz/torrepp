cmake_minimum_required(VERSION 3.7.0)

project(torrepp CXX)
set(PROJECT_NAME TORREPP)

# include build option flags
include(cmake/build_options.cmake)

# turn on test coverage
if(TEST_COVERAGE)
    set(COVERAGE_FLAGS "--coverage")
else()
    set(COVERAGE_FLAGS "")
endif()

# add library target
add_library(torrepp INTERFACE)
file(GLOB_RECURSE TORREPP_FILES torrepp/*.h)
target_sources(torrepp INTERFACE ${TORREPP_FILES})
target_include_directories(torrepp INTERFACE torrepp/)
include(cmake/compiler_warnings.cmake)
set_project_warnings(torrepp INTERFACE)

# Compiler Flags
set(CMAKE_CXX_STANDARD 17)
if (CMAKE_COMPILER_IS_GNUCXX)
    set(CMAKE_CXX_FLAGS "-std=c++17 -O3 -fPIC -funroll-loops -march=native ${COVERAGE_FLAGS}")
elseif (MSVC)
    # this currently works, but is not really the way to go..
    set(CMAKE_CXX_FLAGS "/std:c++17 /Wall /arch:AVX")
else ()
    set(CMAKE_CXX_FLAGS "-std=c++17 -O3 -fPIC -funroll-loops -march=native -fno-finite-math-only -fno-signed-zeros -freciprocal-math -ffp-contract=fast")
endif (CMAKE_COMPILER_IS_GNUCXX)

if (FORCE_COLOR_OUTPUT)
    if (CMAKE_COMPILER_IS_GNUCXX)
        add_compile_options(-fdiagnostics-color=always)
    else ()
        add_compile_options(-fcolor-diagnostics)
    endif ()
endif (FORCE_COLOR_OUTPUT)

include(CheckCXXCompilerFlag)
include(GNUInstallDirs)

find_package(Threads)

if (${PROJECT_NAME}_ENABLE_OMP)
    find_package(OpenMP)
    if (OpenMP_CXX_FOUND)
        set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
        link_libraries(OpenMP::OpenMP_CXX)
        include_directories(${OpenMP_CXX_INCLUDE_DIRS})
    endif ()
endif ()

if (${PROJECT_NAME}_BUILD_TEST)
    enable_testing()
    add_subdirectory(test)
endif ()

add_subdirectory(app)

set(TORREPP_VERSION_NUMBER 21.3.19)
set(TORREPP_VERSION_STRING ${TORREPP_VERSION_NUMBER})
set(TORREPP_DEFINITIONS "")
set(TORREPP_INCLUDE_DIR "${CMAKE_INSTALL_PREFIX}/include")
set(TORREPP_ROOT_DIR ${CMAKE_INSTALL_PREFIX})

include(CMakePackageConfigHelpers)

configure_package_config_file(
        ${CMAKE_CURRENT_SOURCE_DIR}/cmake/torrepp.cmake.in
        ${CMAKE_CURRENT_BINARY_DIR}/torreppConfig.cmake
        PATH_VARS TORREPP_INCLUDE_DIR TORREPP_ROOT_DIR
        INSTALL_DESTINATION ${CMAKE_INSTALL_DATADIR}/torrepp/cmake
        NO_CHECK_REQUIRED_COMPONENTS_MACRO)

write_basic_package_version_file(torreppConfigVersion.cmake VERSION ${TORREPP_VERSION_NUMBER} COMPATIBILITY SameMajorVersion)
install(FILES ${CMAKE_CURRENT_BINARY_DIR}/torreppConfig.cmake ${CMAKE_CURRENT_BINARY_DIR}/torreppConfigVersion.cmake DESTINATION ${CMAKE_INSTALL_DATADIR}/torrepp/cmake)
install(DIRECTORY torrepp DESTINATION include)




