cmake_minimum_required(VERSION 2.4)

# name of the project (dummy)
project(ftmTreeCmd)

set(CMAKE_CXX_FLAGS "-D_GLIBCXX_PARALLEL")

# command-line build-mode
set(TTK_BUILD_MODE "VTK-CMD")

# path to the common code base
find_path(TTK_DIR ttk.cmake
  PATHS
    core/
    ../core/
    ../../core/
    ../../../core/
)
include(${TTK_DIR}/ttk.cmake)

# Special build for perf, don't create the result data set
option(PERF_TESTS  "Build only for performances, avoid post-process" OFF)
if(PERF_TESTS)
   add_definitions(-DPERF_TESTS)
endif(PERF_TESTS)

# include the different packages required for the application
ttk_add_vtkWrapper_package(ttkFTMTree)

# add the local cpp files
ttk_add_source(Editor.cpp)
ttk_add_source(main.cpp)

# wrap-up the build
ttk_wrapup_binary(ftmTreeCmd)
