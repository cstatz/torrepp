set(BUILD_TARGET "forward")

include_directories(${CMAKE_SOURCE_DIR} "/usr/local/include")

#file(GLOB SOURCES "*.cc" "${CMAKE_SOURCE_DIR}/examples/common/cnpy.cc")
add_executable(${BUILD_TARGET} ${SOURCES})
message(${SOURCES})

#find_package(nlohmann_json 3.2.0 REQUIRED)
#find_package(ZLIB REQUIRED)
#target_include_directories(${BUILD_TARGET} PUBLIC ${ZLIB_INCLUDE_DIRS})

#target_link_libraries(${BUILD_TARGET} PUBLIC nlohmann_json::nlohmann_json ${ZLIB_LIBRARIES})

IF (OpenMP_CXX_FOUND)
    target_link_libraries(${BUILD_TARGET} PUBLIC OpenMP::OpenMP_CXX)
ENDIF ()

source_group("Source Files" FILES ${SOURCES})
