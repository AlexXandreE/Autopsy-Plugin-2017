#
# To build project 
#

#cmake --build . --config Release
#cmake -G "Visual Studio 14 2015 Win64" -T host=x64 ..

# Dlib minimum recommended version -> 2.8.12
cmake_minimum_required(VERSION 2.8.12)

set(CMAKE_BUILD_TYPE Release)

# Project name
project(FDRV)


# Include Dlib into the project
# TODO: Make this generic, it's just for my build
add_subdirectory("C:\\Users\\Alexandre\\libs\\dlib" dlib_build)
add_subdirectory("C:\\Users\\Alexandre\\libs\\pugixml-1.9" pugi_build)

set(BOOST_LIBRARYDIR "C:\\Users\\Alexandre\\libs\\boost_1_68_0\\stage\\lib")
set(Boost_USE_STATIC_LIBS ON)

# TODO: Make this generic, it's just for my build
set(OPENSSL_ROOT_DIR "C:\\Users\\Alexandre\\libs\\openssl-1.1.1a")
set(OPENSSL_USE_STATIC_LIBS TRUE)

find_package(OpenSSL REQUIRED)
find_package(Boost 1.68.0 COMPONENTS filesystem date_time program_options REQUIRED)

include_directories(${Boost_INCLUDE_DIR})

# TODO: Make this generic, it's just for my build
set(OpenCV_DIR "C:/Users/Alexandre/libs/opencv-4.0.0/build/")
find_package(OpenCV REQUIRED)

include_directories(./include ./src )

add_executable(FDRV main2.cpp ./src/image_handling.cpp src/helper_functions.cpp ./src/DFXML_creator.cpp src/structs.cpp)

# Aditional libraries
target_link_libraries(FDRV dlib::dlib)
target_link_libraries(FDRV Boost::filesystem Boost::date_time Boost::program_options)
target_link_libraries(FDRV ${OpenCV_LIBS})
target_link_libraries(FDRV OpenSSL::Crypto)
target_link_libraries(FDRV pugixml)
