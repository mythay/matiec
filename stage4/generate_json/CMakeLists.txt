add_library(stage4_json STATIC generate_json.cc)
target_include_directories(stage4_json PUBLIC ${CMAKE_CURRENT_SOURCE_DIR} ../../..)
target_link_libraries(stage4_json PRIVATE stage4)