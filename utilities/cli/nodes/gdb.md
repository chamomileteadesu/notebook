# gdb

> GNU 调试器，用于调试程序。
> 更多信息：<https://manned.org/gdb>

- 调试可执行文件：
  `gdb {{可执行文件}}`

- 调试运行中的进程：
  `gdb -p {{PID}}`

- 启动时设置断点：
  `gdb --ex "break {{main}}" {{可执行文件}}`

- 运行程序（在 gdb 中）：
  `run`

- 在指定行设置断点：
  `break {{文件名}}:{{行号}}`

- 在函数处设置断点：
  `break {{函数名}}`

- 单步执行（不进入函数）：
  `next`

- 单步执行（进入函数）：
  `step`

- 继续运行直到下一个断点：
  `continue`

- 打印变量值：
  `print {{变量名}}`

- 查看调用栈：
  `backtrace`

- 退出调试：
  `quit`
