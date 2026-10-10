# dust

> du 的现代化替代品，更直观的磁盘使用分析工具。
> 更多信息：<https://github.com/bootandy/dust>

- 显示当前目录的磁盘使用情况：
  `dust`

- 显示指定目录的磁盘使用情况：
  `dust {{路径}}`

- 限制显示深度：
  `dust --depth {{N}}`

- 只显示前 N 个最大的目录/文件：
  `dust --number-of-lines {{N}}`

- 排除某些目录：
  `dust --ignore-directory {{node_modules}}`

- 反向排序（从小到大）：
  `dust --reverse`
