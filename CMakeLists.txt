cmake_minimum_required (VERSION 3.5)

#---------------------------------------- Project ----------------------------------------
project (cpptest)

# Version
set (VERSION_MAJOR 0)
set (VERSION_MINOR 0)
set (VERSION_PATCH 1)

# Disable in-source builds to prevent source tree corruption.
if(" ${CMAKE_SOURCE_DIR}" STREQUAL " ${CMAKE_BINARY_DIR}")
  message(FATAL_ERROR "
FATAL: In-source builds are not allowed.
       You should create a separate directory for build files.
")
endif()

#---------------------------------------- Options ----------------------------------------
option(BUILD_TESTS   "Build tests in every make" ON)

#---------------------------------------- Settings ---------------------------------------
# Output directory settings
set(output_dir ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${output_dir})

# -std=c++1z or -std=gnu++1z
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

#---------------------------------------- Packages ---------------------------------------
# find boost
find_package(Boost 1.71 REQUIRED COMPONENTS
    filesystem
    program_options
    regex
    thread
)

# find google test 
find_package(GTest REQUIRED)


#---------------------------------------- Directories ------------------------------------
# add the CMakeLists.txt files located in subdirectories
add_subdirectory(source)
if(BUILD_TESTS)
	add_subdirectory(tests)
endif()
