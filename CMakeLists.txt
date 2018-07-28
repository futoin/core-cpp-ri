
cmake_minimum_required(VERSION 3.2 FATAL_ERROR)

#--------------------------------------
# Hunter init
#--------------------------------------

include("cmake/HunterGate.cmake")

HunterGate(
    URL "https://github.com/ruslo/hunter/archive/v0.23.1.tar.gz"
    SHA1 "51d2d6be411251c8de18c4ca20ef778880cf4cce"
)

add_subdirectory(externals/core-cpp-api ${CMAKE_BINARY_DIR}/futoin_api)
add_subdirectory(externals/core-cpp-ri-asyncsteps ${CMAKE_BINARY_DIR}/futoin_asyncsteps)

#--------------------------------------
# Project definition
#--------------------------------------

project(futoin_core_ri
        VERSION "0.0.1"
        LANGUAGES CXX)

# Options
#-----
option(FUTOIN_WITH_TESTS "Build with tests" ON)
option(FUTOIN_WITH_DOCS "Build documentation" ON)

#--------------------------------------
# Build documentation
#--------------------------------------
if (FUTOIN_API_WITH_DOCS AND False)
    find_package(Doxygen REQUIRED dot)
    
    add_custom_target(
        docs-asyncsteps ALL
        COMMAND ${DOXYGEN_EXECUTABLE}
        WORKING_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}
    )
    # prevent Doxygen segfault on invalid code
    add_dependencies(docs ${PROJECT_NAME})
endif()

#--------------------------------------
