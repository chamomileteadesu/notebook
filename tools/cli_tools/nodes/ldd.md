# ldd

> 查看可执行文件或共享库依赖的共享库。  
> 更多信息：<https://manned.org/ldd>

- 查看程序依赖：

  `ldd path/to/binary`

- 查看共享库依赖：

  `ldd path/to/lib`

- 显示未使用的直接依赖：

  `ldd [-u|--unused] path/to/binary`

- 详细输出：

  `ldd [-v|--verbose] path/to/binary`

- 检查数据相关的依赖是否完整:

  `ldd [-d|--data-relocs] path/to/binary`

- 检查数据、函數相关的依赖是否完整:

  `ldd [-r|--function-relocs] path/to/binary`
