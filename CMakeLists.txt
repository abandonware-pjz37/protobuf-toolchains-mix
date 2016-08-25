cmake_minimum_required(VERSION 3.0)

include("cmake/HunterGate.cmake")
HunterGate(
    URL "https://github.com/ruslo/hunter/archive/v0.15.19.tar.gz"
    SHA1 "899dd70ac66e2c4962386a0497a49c1b50f98b1e"
)

project(download-Protobuf)

# If we cross compile for Android or iOS build a separate protoc executable on host to compile .proto files in CMake
if(IOS OR ANDROID)
  include(hunter_experimental_add_host_project)
  hunter_experimental_add_host_project(cmake/host)

  add_executable(protobuf::protoc IMPORTED)
  set_target_properties(protobuf::protoc PROPERTIES IMPORTED_LOCATION "${HUNTER_HOST_ROOT}/bin/protoc")
endif(IOS OR ANDROID)

hunter_add_package(Protobuf)

find_package(Protobuf CONFIG REQUIRED)

add_subdirectory(messages)

add_executable(hello main.cpp)
target_link_libraries(hello messages)
