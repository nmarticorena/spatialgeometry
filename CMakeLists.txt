cmake_minimum_required(VERSION 3.25)
project(spatialgeometry LANGUAGES CXX)

# Python + NumPy
find_package(Python COMPONENTS Interpreter Development.Module NumPy REQUIRED)

Python_add_library(scene MODULE
    spatialgeometry/core/scene.cpp
    WITH_SOABI)
target_compile_features(scene PRIVATE cxx_std_17)
target_include_directories(scene PRIVATE
    ${Python_NumPy_INCLUDE_DIRS}
    ${CMAKE_CURRENT_SOURCE_DIR}/spatialgeometry/core
)
target_link_libraries(scene PRIVATE Python::Module Python::NumPy)


install(TARGETS scene LIBRARY DESTINATION spatialgeometry)
