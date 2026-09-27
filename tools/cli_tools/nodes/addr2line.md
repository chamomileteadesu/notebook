# addr2line

> 将程序地址转换为源代码行号和函数名。
> 更多信息：<https://manned.org/addr2line>

- 将地址转换为行号：
  `addr2line -e {{可执行文件}} {{地址}}`

- 显示函数名：
  `addr2line -f -e {{可执行文件}} {{地址}}`

- 同时显示函数名和行号：
  `addr2line -f -e {{可执行文件}} {{地址}}`

- 处理多个地址：
  `addr2line -e {{可执行文件}} {{地址1}} {{地址2}} {{地址3}}`

- 从标准输入读取地址：
  `echo "{{地址}}" | addr2line -e {{可执行文件}}`

- 显示地址的详细调试信息：
  `addr2line -i -e {{可执行文件}} {{地址}}`

- 解析共享库中的地址：
  `addr2line -e {{共享库.so}} {{地址}}`

- 使用内核调试符号：
  `addr2line -e {{内核镜像}} {{内核地址}}`

- 解析静态库中的地址：
  `addr2line -e {{静态库.a}} {{地址}}`

- 显示内联函数信息：
  `addr2line -i -e {{可执行文件}} {{地址}}`

- 从堆栈跟踪解析地址：
  `addr2line -e {{可执行文件}} -f -i {{地址列表}}`

- 解析 Core Dump 中的地址：
  `addr2line -e {{可执行文件}} -f -i < {{地址文件}}`

- 解析特定偏移量的地址：
  `addr2line -e {{可执行文件}} -j {{段名}} {{偏移量}}`

- 显示地址的绝对路径：
  `addr2line -e {{可执行文件}} -a {{地址}}`

- 处理十六进制地址：
  `addr2line -e {{可执行文件}} 0x{{十六进制地址}}`

- 批量解析地址：
  `cat {{地址文件}} | addr2line -e {{可执行文件}} -f -i`

- 解析带调试信息的可执行文件：
  `addr2line -e {{调试版本}} {{地址}}`

- 解析带符号表的文件：
  `addr2line -e {{带符号文件}} {{地址}}`

- 显示地址的模块信息：
  `addr2line -e {{可执行文件}} --demangle {{地址}}`

- 处理 C++ 符号：
  `addr2line -e {{C++可执行文件}} -f -C {{地址}}`

- 从 GDB 输出解析地址：
  `gdb -batch -ex "info proc mappings" {{进程ID}} | addr2line -e {{可执行文件}}`

- 解析 JIT 编译的地址：
  `addr2line -e {{JIT代码}} -f -i {{地址}}`

- 显示地址的源代码上下文：
  `addr2line -e {{可执行文件}} -f -i -p {{地址}}`

- 解析特定库的地址：
  `addr2line -e {{库名}} {{地址}}`

- 处理分割的地址空间：
  `addr2line -e {{可执行文件}} --basenames {{地址}}`

- 解析内核模块地址：
  `addr2line -e {{内核模块.ko}} {{模块地址}}`

- 显示地址的函数调用层次：
  `addr2line -e {{可执行文件}} -i -p {{地址}}`

- 解析优化后的代码地址：
  `addr2line -e {{优化版本}} -f -i {{地址}}`

- 处理地址列表文件：
  `addr2line -e {{可执行文件}} -f -i < {{地址列表文件}}`

- 解析带调试信息的共享库：
  `addr2line -e {{调试共享库.so}} {{地址}}`

- 显示地址的行号范围：
  `addr2line -e {{可执行文件}} --functions {{地址}}`

- 解析特定函数的地址范围：
  `objdump -t {{可执行文件}} | grep {{函数名}} | addr2line -e {{可执行文件}}`

- 处理 Core Dump 的完整堆栈：
  `gdb -batch -ex "bt full" {{可执行文件}} {{core文件}} | grep "#[0-9]" | awk '{print $3}' | addr2line -e {{可执行文件}} -f -i`

- 解析 Java JNI 地址：
  `addr2line -e {{JNI库.so}} {{JNI地址}}`

- 显示地址的汇编对应关系：
  `addr2line -e {{可执行文件}} {{地址}} && objdump -d {{可执行文件}} | grep -A 5 {{地址}}`

- 解析 Python 扩展模块地址：
  `addr2line -e {{Python扩展.so}} {{地址}}`

- 处理地址格式化输出：
  `addr2line -e {{可执行文件}} -f -i -p {{地址}} | awk -F: '{print "Function:", $1, "File:", $2, "Line:", $3}'`

- 解析 Rust 程序地址：
  `addr2line -e {{Rust可执行文件}} -f -i {{地址}}`

- 显示地址的内存映射信息：
  `addr2line -e {{可执行文件}} --pretty {{地址}}`

- 解析 Go 程序地址：
  `addr2line -e {{Go程序}} -f -i {{地址}}`
