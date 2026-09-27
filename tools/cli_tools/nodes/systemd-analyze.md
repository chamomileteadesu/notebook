# systemd-analyze

> 分析系统启动性能和 Systemd 状态。
> 更多信息：<https://manned.org/systemd-analyze>

- 显示上次启动所花时间：
  `systemd-analyze`

- 显示各服务启动时间（按耗时排序）：
  `systemd-analyze blame`

- 显示关键启动链：
  `systemd-analyze critical-chain`

- 生成启动时间分析图（SVG 格式）：
  `systemd-analyze plot > {{启动分析.svg}}`

- 生成启动时间瀑布图：
  `systemd-analyze plot --json=pretty`

- 分析特定服务的启动时间：
  `systemd-analyze critical-chain {{服务名.service}}`

- 验证单元文件语法：
  `systemd-analyze verify {{单元文件路径}}`

- 显示当前单元文件的计算配置：
  `systemd-analyze cat-config {{单元名}}`

- 生成单元依赖关系图：
  `systemd-analyze dot {{单元名}} | dot -Tsvg > {{依赖图.svg}}`

- 列出所有单元的依赖关系：
  `systemd-analyze list-dependencies`

- 列出特定单元的依赖关系：
  `systemd-analyze list-dependencies {{服务名.service}}`

- 测量命令启动时间：
  `systemd-analyze time {{命令}}`