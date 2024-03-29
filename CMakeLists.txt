
cmake_minimum_required(VERSION 3.3 FATAL_ERROR)

#--------------------------------------
# Hunter init
#--------------------------------------

include("cmake/HunterGate.cmake")

HunterGate(
    URL "https://github.com/cpp-pm/hunter/archive/v0.24.16.tar.gz"
    SHA1 "09668c254f01afeca1b3d3d2e4692ed5e0e39dcc"
    LOCAL
)

add_subdirectory(externals/core-cpp-api)
add_subdirectory(externals/core-cpp-ri-asyncsteps)
add_subdirectory(externals/core-cpp-ri-asyncevent)

#--------------------------------------
# Project definition
#--------------------------------------

project(futoin_core_ri
        VERSION "0.3.2" # AUTO-REPLACE
        LANGUAGES CXX)

# Options
#-----
option(FUTOIN_WITH_TESTS "Build with tests" ON)
option(FUTOIN_WITH_DOCS "Build documentation" ON)

#--------------------------------------
# Build documentation
#--------------------------------------
if (FUTOIN_WITH_DOCS AND FALSE)
    find_package(Doxygen REQUIRED dot)
    
    add_custom_target(
        docs-futoin ALL
        COMMAND ${CMAKE_COMMAND} -E env "BUILD_DIR=${CMAKE_CURRENT_BINARY_DIR}" ${DOXYGEN_EXECUTABLE}
        WORKING_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}
    )
endif()

#--------------------------------------
if (FUTOIN_WITH_TESTS)
    # Note: this stuff must be called in root CMakeLists.txt
    # to make "test" target available.
    include(CTest)

    enable_testing()
endif()
