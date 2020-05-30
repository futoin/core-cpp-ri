
cmake_minimum_required(VERSION 3.3 FATAL_ERROR)

#--------------------------------------
# Hunter init
#--------------------------------------

include("cmake/HunterGate.cmake")

HunterGate(
    URL "https://github.com/cpp-pm/hunter/archive/v0.23.255.tar.gz"
    SHA1 "e2ab1e33fa99b8481ec5c7ee6314195d34826e7d"
)

add_subdirectory(externals/core-cpp-api)
add_subdirectory(externals/core-cpp-ri-asyncsteps)
add_subdirectory(externals/core-cpp-ri-asyncevent)

#--------------------------------------
# Project definition
#--------------------------------------

project(futoin_core_ri
        VERSION "0.2.1" # AUTO-REPLACE
        LANGUAGES CXX)

# Options
#-----
option(FUTOIN_WITH_TESTS "Build with tests" ON)
option(FUTOIN_WITH_DOCS "Build documentation" ON)

#--------------------------------------
# Build documentation
#--------------------------------------
if (FUTOIN_WITH_DOCSAND AND FALSE)
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
