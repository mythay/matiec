find_package(BISON REQUIRED)
find_package(FLEX REQUIRED)

# 生成 bison 和 flex 源文件
BISON_TARGET(Parser iec_bison.yy ${CMAKE_CURRENT_BINARY_DIR}/iec_bison.cc DEFINES_FILE ${CMAKE_CURRENT_BINARY_DIR}/iec_bison.hh)
FLEX_TARGET(Lexer iec_flex.ll ${CMAKE_CURRENT_BINARY_DIR}/iec_flex.cc)
ADD_FLEX_BISON_DEPENDENCY(Lexer Parser)

add_library(stage1_2 STATIC
    ${BISON_Parser_OUTPUTS}
    ${FLEX_Lexer_OUTPUTS}
    create_enumtype_conversion_functions.cc
    stage1_2.cc
)
target_include_directories(stage1_2 PUBLIC ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_BINARY_DIR} ../../absyntax)
target_compile_definitions(stage1_2 PRIVATE DEFAULT_LIBDIR="lib" YY_BUF_SIZE=65536)