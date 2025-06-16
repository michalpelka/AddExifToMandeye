cmake_minimum_required(VERSION 3.28)
project(AddExifToMandeye)

include(FetchContent)

FetchContent_Declare(
        exiv2
        GIT_REPOSITORY https://github.com/Exiv2/exiv2.git
        GIT_TAG v0.28.2
)

set(CMAKE_CXX_STANDARD 20)
set(BUILD_SHARED_LIBS OFF CACHE BOOL "" FORCE)
set(EXIV2_ENABLE_INIH OFF CACHE BOOL "" FORCE)
set(EXIV2_BUILD_UNIT_TESTS OFF CACHE BOOL "" FORCE)
set(EXIV2_BUILD_SAMPLES OFF CACHE BOOL "" FORCE)
set(EXIV2_BUILD_EXIV2_COMMAND OFF CACHE BOOL "" FORCE)
set(EXIV2_INSTALL ON CACHE BOOL "" FORCE)
set(EXIV2_ENABLE_BROTLI OFF CACHE BOOL "" FORCE)
set(EXIV2_ENABLE_PNG OFF CACHE BOOL "" FORCE)
set(EXIV2_ENABLE_XMP OFF CACHE BOOL "" FORCE)
# Make available
FetchContent_MakeAvailable(exiv2)

add_executable(add_exif_to_photos add_exif_to_photots.cpp)
target_include_directories(add_exif_to_photos PRIVATE ${CMAKE_BINARY_DIR}) # For the generated exiv2lib_export.h
target_link_libraries(add_exif_to_photos PRIVATE exiv2lib)

install (TARGETS add_exif_to_photos
        RUNTIME DESTINATION bin
        LIBRARY DESTINATION lib
        ARCHIVE DESTINATION lib)

# pack zip
set(CPACK_GENERATOR "ZIP")
set(CPACK_PACKAGE_NAME "AddExifToMandeye")

include(CPack)