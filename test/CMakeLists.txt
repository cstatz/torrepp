file(GLOB_RECURSE TEST_SRC ${CMAKE_SOURCE_DIR}/test/*.cpp)


add_executable(test_torrepp ${TEST_SRC} ${EMBREE_PRIMITIVES_SRC})
target_include_directories(test_torrepp PUBLIC ${CMAKE_SOURCE_DIR} ${EMBREE_INCLUDE_DIRS} ${BLAZE_INCLUDE_DIRS} "/usr/local/include")
target_link_libraries(test_torrepp PUBLIC ${EMBREE_LIBRARY})
target_link_libraries(test_torrepp PRIVATE torrepp)

set_target_properties(test_torrepp PROPERTIES LINKER_LANGUAGE CXX)
add_test(main test_torrepp)

# standard compiler warnings
include(../cmake/compiler_warnings.cmake)
set_project_warnings(test_torrepp PRIVATE)
