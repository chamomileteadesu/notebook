# watch

> 周期性执行命令并显示输出。
> 更多信息：<https://manned.org/watch>

- 每隔 2 秒执行命令（默认间隔）：
  `watch {{命令}}`

- 指定执行间隔（秒）：
  `watch -n {{秒数}} {{命令}}`

- 高亮显示变化部分：
  `watch -d {{命令}}`

- 精确高亮变化（即使快速变化也能显示）：
  `watch -d=cumulative {{命令}}`

- 不显示标题栏：
  `watch -t {{命令}}`

- 在命令出错时退出：
  `watch -e {{命令}}`

- 监控文件系统变化：
  `watch -n 1 "ls -la"`
