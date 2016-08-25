cmake_minimum_required(VERSION 3.0)

include("../HunterGate.cmake")
HunterGate(
    URL "${HUNTER_HOST_URL}"
    SHA1 "${HUNTER_HOST_SHA1}"
)

project(download-Protobuf-host)

hunter_add_package(Protobuf)
