# networkctl

> 查询和控制在 systemd-networkd 中的网络连接。
> 更多信息：<https://manned.org/networkctl>

- 列出所有网络连接：
  `networkctl list`

- 显示网络连接详情：
  `networkctl status`

- 显示指定网络接口详情：
  `networkctl status {{接口名}}`

- 启用网络接口：
  `networkctl up {{接口名}}`

- 禁用网络接口：
  `networkctl down {{接口名}}`

- 重新加载网络配置：
  `networkctl reload`

- 重新配置网络接口：
  `networkctl reconfigure {{接口名}}`

- 显示网络接口统计信息：
  `networkctl stats {{接口名}}`

- 显示所有链路层信息：
  `networkctl lldp`

- 启用 DHCP：
  `networkctl renew {{接口名}}`

- 删除 IPv6 动态地址：
  `networkctl delete {{接口名}}`

- 查看网络配置文件路径：
  `networkctl cat {{接口名}}`
