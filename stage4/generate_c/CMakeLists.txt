add_library(stage4_c STATIC generate_c.cc)
target_include_directories(stage4_c PUBLIC ${CMAKE_CURRENT_SOURCE_DIR} ../../..)
target_link_libraries(stage4_c PRIVATE stage4)