cmake_minimum_required(VERSION 3.10)
project(matiec CXX)

# 设置 C++ 标准
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


add_definitions(-DPACKAGE_NAME=\"matiec\" -DPACKAGE_VERSION=\"0.2.1\")


# 包含子目录
add_subdirectory(absyntax)
add_subdirectory(absyntax_utils)
add_subdirectory(stage1_2)
add_subdirectory(stage3)
add_subdirectory(stage4)

# 主程序源文件
set(MAIN_SRC main.cc)

# 生成 iec2c
add_executable(iec2c ${MAIN_SRC})
target_link_libraries(iec2c PRIVATE  stage1_2 stage3 stage4_c absyntax absyntax_utils)

# 生成 iec2iec
add_executable(iec2iec ${MAIN_SRC})
target_link_libraries(iec2iec PRIVATE  stage1_2 stage3 stage4_iec absyntax absyntax_utils)

# 生成 iec2json
add_executable(iec2json ${MAIN_SRC})
target_link_libraries(iec2json PRIVATE  stage1_2 stage3 stage4_json absyntax absyntax_utils)

# 包含头文件目录
# target_include_directories(iec2c PRIVATE absyntax absyntax_utils stage1_2 stage3 stage4)
# target_include_directories(iec2iec PRIVATE absyntax absyntax_utils stage1_2 stage3 stage4)
# target_include_directories(iec2json PRIVATE absyntax absyntax_utils stage1_2 stage3 stage4)



if(CMAKE_CXX_COMPILER MATCHES ".*mingw.*")
    message("Static linking on MinGW")
    target_link_options(iec2c PRIVATE -static)
    target_link_options(iec2iec PRIVATE -static)
    target_link_options(iec2json PRIVATE -static)
endif()