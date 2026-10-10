# systemd-cgtop

> 实时显示 Cgroup 资源使用情况（类似 top 命令）。
> 更多信息：<https://manned.org/systemd-cgtop>

- 显示所有 cgroup 的资源使用情况：
  `systemd-cgtop`

- 按指定顺序排序（task、cpu、memory、io）：
  `systemd-cgtop --order={{cpu}}`

- 仅显示指定 cgroup：
  `systemd-cgtop {{system.slice}}`

- 显示用户会话的资源使用：
  `systemd-cgtop user.slice`

- 设置刷新间隔（秒）：
  `systemd-cgtop --delay={{2}}`

- 仅显示 CPU 使用率：
  `systemd-cgtop --cpu`

- 以批处理模式运行（适合管道或脚本）：
  `systemd-cgtop --batch`

- 批处理模式下指定迭代次数：
  `systemd-cgtop --batch --iterations={{5}}`

- 显示完整的单元名称：
  `systemd-cgtop --full`

- 显示深度限制的 cgroup 层级：
  `systemd-cgtop --depth={{2}}`