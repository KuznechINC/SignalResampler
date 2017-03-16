cmake_minimum_required(VERSION 3.2)

project(Resampler)

find_package(Boost REQUIRED)

add_library(Resampler src/resample.cpp)
target_include_directories(Resampler
        PUBLIC
        "$<BUILD_INTERFACE:${CMAKE_CURRENT_LIST_DIR}/include>"
)
set_property(TARGET Resampler PROPERTY POSITION_INDEPENDENT_CODE ON)

set(targets_export_name "ResamplerTargets")
set(generated_dir "${CMAKE_CURRENT_BINARY_DIR}/generated")
include(CMakePackageConfigHelpers)
configure_package_config_file(
        "cmake/Config.cmake.in"
        "${generated_dir}/ResamplerConfig.cmake"
        INSTALL_DESTINATION "lib/cmake/Resampler"
)

# install the binaries and include files
install(TARGETS Resampler
        EXPORT "${targets_export_name}"
        ARCHIVE DESTINATION lib
        LIBRARY DESTINATION lib
        INCLUDES DESTINATION "include")

install(FILES "include/resample.h" DESTINATION include/resampler)

# Config
#   * <prefix>/lib/cmake/Foo/FooConfig.cmake
#   * <prefix>/lib/cmake/Foo/FooConfigVersion.cmake
install(
        FILES "${generated_dir}/ResamplerConfig.cmake"
        DESTINATION "lib/cmake/Resampler"
)

# Config
#   * <prefix>/lib/cmake/Foo/FooTargets.cmake
install(
        EXPORT "${targets_export_name}"
        DESTINATION "lib/cmake/Resampler"
)
