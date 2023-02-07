cmake_minimum_required(VERSION 3.22)
project(ode_poc C)

set(CMAKE_C_STANDARD 17)

include(FetchContent)
if(NOT ODE_LOCATION)
    set(ODE_LOCATION https://bitbucket.org/odedevs/ode.git)
endif()
FetchContent_Declare(
    ode
    GIT_REPOSITORY ${ODE_LOCATION}
    GIT_TAG master
)
FetchContent_GetProperties(ode)
if(NOT ode_POPULATED)
    FetchContent_Populate(ode)
    add_subdirectory(${ode_SOURCE_DIR} ${ode_BINARY_DIR} EXCLUDE_FROM_ALL)
endif()

add_executable(ode_poc main.c)
target_include_directories(ode_poc PRIVATE ${ode_SOURCE_DIR}/include)
