cmake_minimum_required(VERSION 3.1)
project(learnSPH)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DUSE_DOUBLE -fopenmp")
if (NOT CMAKE_BUILD_TYPE)
	set(CMAKE_BUILD_TYPE "DEBUG")
endif()

if (CMAKE_BUILD_TYPE MATCHES "DEBUG")
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DDEBUG")
endif()

if (CMAKE_BUILD_TYPE MATCHES "RELEASE")
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -DPROFILE")
endif()


if (MSVC)
  set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /MP") # Parallel compilation in Visual Studio
endif()

include_directories("${CMAKE_SOURCE_DIR}/include/"
					 "${CMAKE_SOURCE_DIR}/extern/Eigen/")

# Modules
add_subdirectory(learnSPH)
add_subdirectory(app)
add_subdirectory(CompactNSearch)

# Copy res folder
file(MAKE_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/res)

