cmake_minimum_required(VERSION 3.8.0)

project (mender_demo C CXX)

include(${CMAKE_CURRENT_BINARY_DIR}/conanbuildinfo.cmake OPTIONAL RESULT_VARIABLE HAS_CONAN)
if (NOT HAS_CONAN)
  message(FATAL_ERROR "missing conanbuildinfo.cmake did you forget to run conan install ?")
endif()
conan_basic_setup()

include(os)

os_add_executable(mender_demo "IncludeOS Mender Example" service.cpp)
os_add_drivers(mender_demo virtionet vmxnet3)

os_diskbuilder(mender_demo disk)
