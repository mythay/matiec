add_library(stage4 STATIC stage4.cc)
target_include_directories(stage4 PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

# 添加子目录
add_subdirectory(generate_c)
add_subdirectory(generate_iec)
add_subdirectory(generate_json)