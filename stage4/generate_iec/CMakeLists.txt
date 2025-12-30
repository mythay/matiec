add_library(stage4_iec STATIC generate_iec.cc)
target_include_directories(stage4_iec PUBLIC ${CMAKE_CURRENT_SOURCE_DIR} ../../..)
target_link_libraries(stage4_iec PRIVATE stage4)