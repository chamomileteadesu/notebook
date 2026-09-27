# objdump

> 显示目标文件的信息，包括头部、程序头、段和符号表等。
> 更多信息：<https://manned.org/objdump>

- 显示文件头信息：
  `objdump -f {{目标文件}}`

- 显示程序头：
  `objdump -p {{目标文件}}`

- 显示段头部：
  `objdump -h {{目标文件}}`

- 反汇编代码段：
  `objdump -d {{目标文件}}`

- 反汇编所有段：
  `objdump -D {{目标文件}}`

- 显示符号表：
  `objdump -t {{目标文件}}`

- 显示动态符号表：
  `objdump -T {{目标文件}}`

- 显示重定位信息：
  `objdump -r {{目标文件}}`

- 以十六进制格式显示完整内容：
  `objdump -s {{目标文件}}`

- 显示指定段的内容：
  `objdump -j {{段名}} -s {{目标文件}}`

- 显示调试信息：
  `objdump -g {{目标文件}}`

- 显示文件头和程序头：
  `objdump -x {{目标文件}}`

- 显示源代码混合的汇编：
  `objdump -S {{目标文件}}`

- 反汇编并显示源代码行号：
  `objdump -d -l {{目标文件}}`

- 显示架构信息：
  `objdump -i {{目标文件}}`

- 显示动态库依赖：
  `objdump -p {{目标文件}} | grep NEEDED`

- 反汇编指定地址范围：
  `objdump -d --start-address={{起始地址}} --stop-address={{结束地址}} {{目标文件}}`

- 显示特定符号的反汇编：
  `objdump -d {{目标文件}} | grep -A 10 "{{符号名}}"`

- 显示文件的所有信息：
  `objdump --all-headers {{目标文件}}`

- 显示宽格式的反汇编：
  `objdump -d -w {{目标文件}}`

- 显示 Mach-O 文件信息（macOS）：
  `objdump -macho -h {{目标文件}}`

- 显示 ELF 文件的段权限：
  `objdump -h {{目标文件}} | awk '{print $2, $3}'`

- 反汇编并显示操作码：
  `objdump -d --show-raw-insn {{目标文件}}`

- 显示文件的节区头：
  `objdump --section-headers {{目标文件}}`

- 显示文件的符号大小：
  `objdump -t {{目标文件}} | awk '{print $1, $2, $5}'`

- 查看函数的汇编代码：
  `objdump -d {{目标文件}} | grep -A 20 "<{{函数名}}>:"`

- 显示动态链接信息：
  `objdump -p {{目标文件}} | grep -E "(NEEDED|RPATH)"`

- 反汇编并过滤特定指令：
  `objdump -d {{目标文件}} | grep "{{指令模式}}"`

- 显示文件的 ELF 类型和架构：
  `objdump -f {{目标文件}} | grep -E "(architecture|file format)"`

- 查看共享库的导出符号：
  `objdump -T {{共享库}} | grep "{{符号}}"`

- 显示文件的段权限详细信息：
  `objdump -h {{目标文件}} | awk '{print $2, $3, $4, $5}'`

- 反汇编并显示相对地址：
  `objdump -d --adjust-vma={{偏移量}} {{目标文件}}`

- 显示文件的构建 ID：
  `objdump -n {{目标文件}} | grep "Build ID"`

- 查看函数调用关系：
  `objdump -d {{目标文件}} | grep -E "(call|jmp)"`

- 显示文件的节区内容：
  `objdump -j .text -s {{目标文件}}`

- 反汇编并显示字节码：
  `objdump -d --visualize-jumps {{目标文件}}`

- 显示文件的架构特定信息：
  `objdump --file-headers {{目标文件}}`

- 查看静态库的成员：
  `objdump -t {{静态库}} | grep -E "^\."`

- 显示文件的调试符号：
  `objdump --syms {{目标文件}} | grep "{{调试符号}}"`

- 反汇编并显示注释：
  `objdump -d --source-comment {{目标文件}}`

- 显示文件的依赖关系树：
  `objdump -p {{目标文件}} | grep NEEDED | cut -d' ' -f2`

- 查看函数的大小信息：
  `objdump -t {{目标文件}} | grep "{{函数名}}" | awk '{print $5}'`

- 显示文件的段详细信息：
  `objdump --section-headers {{目标文件}} | grep -E "(\.text|\.data|\.bss)"`

- 反汇编并显示控制流图：
  `objdump -d --disassembler-options=att {{目标文件}}`
