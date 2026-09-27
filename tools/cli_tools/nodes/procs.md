# procs

> ps 的现代化替代品，更友好的进程查看工具。
> 更多信息：<https://github.com/dalance/procs>

- 显示所有进程：
  `procs`

- 搜索进程名：
  `procs "{{进程名}}"`

- 查看 PID 对应的进程：
  `procs {{PID}}`

- 显示树形结构：
  `procs --tree`

- 监控模式（持续刷新）：
  `procs --watch`

- 只显示当前用户的进程：
  `procs --user`

- 显示所有列：
  `procs --all`

- 按 CPU 使用率排序：
  `procs --sorta cpu`
