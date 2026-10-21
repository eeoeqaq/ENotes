# CMake 总结

## CMake 是什么

CMake 是一个**跨平台的构建系统生成器**——它不直接编译代码，而是根据 `CMakeLists.txt` 生成各平台的原生构建文件（Unix 的 Makefile、Windows 的 Visual Studio 工程、Ninja 等），再交由这些工具完成编译。

**解决的问题**：直接写 Makefile 或 VS 工程，换平台/换编译器就得重写。CMake 写一次，到处生成。

## 基本写法

一个最小项目结构：

```
project/
├── CMakeLists.txt
├── include/
│   └── mylib.h
├── src/
│   ├── main.cpp
│   └── mylib.cpp
```

```cmake
# 1. 最低版本要求（必须是第一行）
cmake_minimum_required(VERSION 3.16)

# 2. 项目名（可选语言）
project(MyProject CXX)

# 3. 指定 C++ 标准
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 4. 生成可执行文件
add_executable(app src/main.cpp src/mylib.cpp)

# 5. 添加头文件搜索路径
target_include_directories(app PRIVATE include)

# 6. 链接库
find_package(OpenCV REQUIRED)
target_link_libraries(app PRIVATE ${OpenCV_LIBS})
```

## 常用命令速查

| 命令 | 作用 |
|---|---|
| `cmake_minimum_required(VERSION x)` | 声明最低 CMake 版本 |
| `project(Name)` | 定义项目名和语言 |
| `set(VAR value)` | 定义变量，`${VAR}` 引用 |
| `add_executable(name src...)` | 生成可执行文件 |
| `add_library(name STATIC/SHARED src...)` | 生成静态/动态库 |
| `target_include_directories(tgt PRIVATE dir)` | 指定头文件路径 |
| `target_link_libraries(tgt PRIVATE lib)` | 链接库 |
| `add_subdirectory(dir)` | 添加子目录（子目录里放自己的 CMakeLists.txt） |
| `find_package(Pkg REQUIRED)` | 查找外部依赖包 |
| `if()/else()/endif()`、`foreach()` | 条件与循环 |

## PRIVATE / PUBLIC / INTERFACE 的区别

- `PRIVATE`：只给自己用，不传给依赖者
- `PUBLIC`：自己用，也传给链接本库的其他目标
- `INTERFACE`：自己不用，只传给依赖者（典型：纯头文件库）

## 使用流程（out-of-source 构建）

```bash
mkdir build && cd build
cmake ..          # 配置，生成构建文件
cmake --build .   # 编译（等价于 make）
```

注意：**构建产物都放在 `build/` 目录**，源码目录保持干净，清理只需删掉 `build/`。
