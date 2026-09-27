# systemd-cgls

> 以树形结构显示 Cgroup 层次结构。
> 更多信息：<https://manned.org/systemd-cgls>

- 显示整个 cgroup 树：
  `systemd-cgls`

- 显示指定 cgroup 的层次结构：
  `systemd-cgls {{cgroup路径}}`

- 显示所有控制器的 cgroup 层次：
  `systemd-cgls --all`

- 显示指定服务单元的 cgroup：
  `systemd-cgls {{服务名.service}}`

- 显示用户会话的 cgroup：
  `systemd-cgls user.slice`

- 显示系统服务的 cgroup：
  `systemd-cgls system.slice`

- 以 JSON 格式输出：
  `systemd-cgls --json=pretty`

- 显示 cgroup 的详细资源统计：
  `systemd-cgls --full`

- 仅显示指定用户相关的 cgroup：
  `systemd-cgls --user {{用户名}}`