# CMake

## CMake 命令

```sh
# 1. 项目配置
# -S: 指定项目源代码根目录为 .
# -B: 指定构建目录为 ./build
# -G: 告诉 CMake 使用 Ninja 作为构建系统
# -D: 定义 CMake 变量
cmake -S . -B build -G "Ninja" -D SOME_OPTION=ON

# 2. 构建
# --build: 构建产物目录
# -j: 使用多少个线程构建
cmake --build ./build -j 8
```

## CMake 预定义变量

| 变量                      | 备注                             |
| ----                      | ----                             |
| PROJECT_NAME              | 项目名称                         |
| PROJECT_SOURCE_DIR        | 项目根路径                       |
| CMAKE_SOURCE_DIR          | 根级 CMakeLists 所在的路径       |
| CMAKE_CURRENT_SOURCE_DIR  | 当前 CMakeLists 所在的路径       |
| CMAKE_BINARY_DIR          | 构建目录                        |
| CMAKE_BUILD_TYPE          | 设定编译类型                     |
| CMAKE_CXX_FLAG            | C++语言编译器编译选项            |

## CMake 字符串

```txt
# 设置 CMake 变量
set(FOO "foo")

# 字符串拼接
set(new_str str1 str2)

# 字符串追加
list(APPEND ${str} str1 str2)

# 字符串移除
list(REMOVE_ITEM ${str} str1 str2)
```

## CMake 消息

```txt
message(STATUS "[message] 我是一条级别为 STATUS 的消息...")
```

## CMake 基本配置

```cmake
# 最低 CMake 版本要求
cmake_minimum_required(VERSION 3.26)

# 声明项目属性
project(
    # 项目名称
    PROJECT_NAME
    # 项目语言
    LANGUAGES CXX C
    # 项目版本号
    VERSION 0.0.1
    # 项目描述
    DESCRIPTION "..."
)

# 设置 CPP 标准
set(CMAKE_CXX_STANDARD 17)
# 强制使用声明的 CPP 标准
set(CMAKE_CXX_STANDARD_REQUIRED ON)
# 禁用编译器扩展
set(CMAKE_CXX_EXTENSIONS OFF)

# 设置编译器
set(CMAKE_C_COMPILER "/usr/lib/clang")
set(CMAKE_CXX_COMPILER "/usr/bin/clang++")

# 开启如下定义才能让语言服务器正确工作
set(CMAKE_EXPORT_COMPILE_COMMANDS ON CACHE BOOL "Enables compile commands export")

# 为目标指定头文件查找目录
target_include_directories(TARGET PRIVATE "./include")

# 添加源代码
aux_source_directory(${PROJECT_SOURCE_DIR}/src TARGET_SRC)
# or
# file(GLOB TARGET_SRC ${PROJECT_SOURCE_DIR}/src/*.cpp)

# 添加可执行文件目标
add_executable(
    TARGET
    ${TARGET_SRC}
)
```

## 库

```txt
# 指定库输出路径
set(LIBRARY_OUTPUT_PATH ${CMAKE_SOURCE_DIR}/lib)

# 添加库文件目标
add_library(lib_name SHARED|STATLC src)

# 查找 Boost 库，要求版本至少为 1.70.0，并且需要它的 system 组件。
find_package(Boost 1.70.0 REQUIRED COMPONENTS system)

# 链接库到指定目标
target_link_directories(TARGET PUBLIC LIB_DIR)
target_link_libraries(TARGET LIB_NAME)
```

## 其他

```cmakelists
# 设置父节点，父节点的变量对子节点可见，子目录下需要有一个CMakeLists
add_subdirectory(SUB_DIR)

# 为目标添加预处理宏
target_compile_definitions(TARGET PRIVATE -DDEBUG)

# 为一个指定目标添加编译选项
target_compile_options(a.out PUBLIC -Wall -Werror)

# 判断工程是不是顶层工程
if (PROJECT_IS_TOP_LEVEL)
```

## 条件编译

```cmakelists
if(WIN32)
    target_compile_definitions(my_app PRIVATE PLATFORM_WINDOWS)
elseif(UNIX)
    target_compile_definitions(my_app PRIVATE PLATFORM_UNIX)
endif()

# 编译开关，默认为off
option(OPTION_NAME "option description" OFF)
if (OPTION0)
    # ...
endif()
```
