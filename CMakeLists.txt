cmake_minimum_required(VERSION 3.28)
project(nanopb)

find_package(ament_cmake REQUIRED)

# Define a variable for the include directory.
set(nanopb_INCLUDE_DIRS ${CMAKE_CURRENT_SOURCE_DIR}/include)

# Include the headers.
include_directories(${nanopb_INCLUDE_DIRS})

# Create the nanopb_driver library.
add_library(nanopb SHARED
  src/pb_common.c
  src/pb_decode.c
  src/pb_encode.c
)

target_compile_definitions(nanopb PUBLIC "POSIX")

target_include_directories(nanopb PUBLIC
  $<BUILD_INTERFACE:${nanopb_INCLUDE_DIRS}>
  $<INSTALL_INTERFACE:include>
)

# Install headers so that they appear in the "nanopb" subdirectory.
install(DIRECTORY 
  DESTINATION include
)

# Install the library.
install(TARGETS nanopb
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
  RUNTIME DESTINATION bin
)

# Export the include directory and library.
ament_export_include_directories(${nanopb_INCLUDE_DIRS})
ament_export_libraries(nanopb)

ament_package()
