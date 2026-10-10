# strace

> 跟踪系统调用和信号。
> 更多信息：<https://manned.org/strace>

- 跟踪命令的系统调用：
  `strace {{命令}}`

- 跟踪正在运行的进程：
  `sudo strace -p {{PID}}`

- 统计系统调用时间：
  `strace -c {{命令}}`

- 只跟踪特定系统调用：
  `strace -e {{open,read,write}} {{命令}}`

- 跟踪子进程：
  `strace -f {{命令}}`

- 输出到文件：
  `strace -o {{输出文件}} {{命令}}`

- 显示时间戳：
  `strace -t {{命令}}`

- 只跟踪文件操作：
  `strace -e trace=file {{命令}}`
