cmake_minimum_required (VERSION 3.5.1)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


# CMake doc can be found at https://cmake.org/cmake/help/v3.5/

project (BICYCL VERSION 0.0.1 LANGUAGES CXX)
set (BICYCL_DESCRIPTION "BIBYCL Implements CryptographY in CLass groups")

################################################################################
# Add cmake.utils to the list of CMAKE_MODULE_PATH
################################################################################
set (MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/cmake.utils")
list (APPEND CMAKE_MODULE_PATH "${MODULE_DIR}")

set(OPENSSL_ROOT_DIR /usr/local/opt/openssl@3)
set(OPENSSL_LIBRARIES /usr/local/opt/openssl@3/lib)

##############################################################################
# Options for install directory
##############################################################################
set (CMAKE_INSTALL_INCLUDEDIR "include" CACHE PATH "C++ header files (include)")
set (CMAKE_INSTALL_LIBDIR "lib" CACHE PATH "object code libraries (lib)")
set (CMAKE_INSTALL_BINDIR "bin" CACHE PATH "user executables (bin)")
#set (CMAKE_INSTALL_CONFIGCMAKE "share/???/cmake")

##############################################################################
# Print information (to ease debugging)
##############################################################################
message (STATUS "Running on system ${CMAKE_HOST_SYSTEM} with processor ${CMAKE_HOST_SYSTEM_PROCESSOR}")
if (CMAKE_CROSSCOMPILING)
  message (STATUS "Targeting system ${CMAKE_SYSTEM} with processor ${CMAKE_SYSTEM_PROCESSOR}")
endif ()
message (STATUS "Using CMake ${CMAKE_VERSION}")
message (STATUS "C++ compiler: ${CMAKE_CXX_COMPILER_ID} ${CMAKE_CXX_COMPILER_VERSION}")

##############################################################################
# Set C++ standard to c++11
##############################################################################
set (CMAKE_CXX_STANDARD 11)
set (CMAKE_CXX_STANDARD_REQUIRED ON)


##############################################################################
# Options for shared or static library
##############################################################################
option (BUILD_SHARED_LIBS "Set to ON to build shared libraries" OFF)
if (BUILD_SHARED_LIBS)
  message (STATUS "Will build shared libraries")
else ()
  message (STATUS "Will build static libraries")
endif ()

##############################################################################
# Set flags and build type (release or debug)
##############################################################################
if (NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
  message (STATUS "Setting build type to 'Release' as none was specified.")
  set (CMAKE_BUILD_TYPE "Release" CACHE STRING "Choose type of build" FORCE)
  set_property (CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS "Debug" "Release")
endif ()

if(NOT MSVC)
  set (CMAKE_CXX_FLAGS_RELEASE "-O3 -Wall -Wextra -DNDEBUG")
  set (CMAKE_CXX_FLAGS_DEBUG "-O3 -g -Wall -Wextra -DDEBUG")
endif()

################################################################################
# Looking for GMP and OpenSSL
################################################################################
find_package (gmp REQUIRED)
find_package (OpenSSL REQUIRED)

################################################################################
# Looking for thread library
################################################################################
option (WITH_THREADS "Use threads when possible" ON)
if (WITH_THREADS)
  find_package (Threads)
else ()
  message (STATUS "Threads: disabled")
endif ()

################################################################################
# Go to src subdirectory that builds the targets
################################################################################
add_subdirectory (src)

##############################################################################
# add uninstall command
##############################################################################
if(NOT TARGET uninstall)
  set (_infile ${CMAKE_CURRENT_SOURCE_DIR}/cmake.utils/cmake_uninstall.cmake.in)
  set (_outfile ${CMAKE_CURRENT_BINARY_DIR}/cmake_uninstall.cmake)

  configure_file (${_infile} ${_outfile} @ONLY)
  add_custom_target(uninstall COMMAND ${CMAKE_COMMAND} -P ${_outfile})
endif()

find_package (gmp REQUIRED)
find_package (OpenSSL REQUIRED)

include_directories(/usr/local/include/miracl/)
include_directories(/usr/local/lib/)
link_directories(/usr/local/lib/)