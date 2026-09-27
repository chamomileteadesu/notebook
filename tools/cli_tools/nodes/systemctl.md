# systemctl

> Systemd 系统和服务管理器。
> 更多信息：<https://manned.org/systemctl>

- 启动服务：
  `systemctl start {{服务名}}`

- 停止服务：
  `systemctl stop {{服务名}}`

- 重启服务：
  `systemctl restart {{服务名}}`

- 查看服务状态：
  `systemctl status {{服务名}}`

- 启用开机自启：
  `systemctl enable {{服务名}}`

- 禁用开机自启：
  `systemctl disable {{服务名}}`

- 查看所有正在运行的服务：
  `systemctl list-units --type=service --state=running`

- 重新加载 systemd 配置：
  `systemctl daemon-reload`

- 查看服务是否开机自启：
  `systemctl is-enabled {{服务名}}`
