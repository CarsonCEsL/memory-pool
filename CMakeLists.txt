# cmake minimum version
cmake_minimum_required(VERSION 3.10)

# project name and version
project(MemoryPoolProject VERSION 0.1.0 LANGUAGES CXX)

# 让cmake导出编译命令信息，vscode跳转
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# set c++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)

# find header files
include_directories(include)

# 1. 将 src 下的核心代码编译为静态库
file(GLOB SRC_FILES "src/*.cpp")
add_library(memory_pool_lib STATIC ${SRC_FILES})
target_compile_options(memory_pool_lib PRIVATE -g -pthread)

# 2. 编译测试可执行文件
file(GLOB TEST_FILES "tests/*.cpp") 
add_executable(unit_test ${TEST_FILES})

# 让测试程序链接核心代码库以及系统的 pthread 库
target_link_libraries(unit_test PRIVATE memory_pool_lib pthread)