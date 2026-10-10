# ip

> 显示或操作路由、设备、策略路由和隧道（新一代网络配置工具）。
> 更多信息：<https://manned.org/ip>

- 显示 IP 地址：
  `ip addr show`

- 显示指定接口的 IP 地址：
  `ip addr show {{eth0}}`

- 启用网络接口：
  `sudo ip link set {{eth0}} up`

- 禁用网络接口：
  `sudo ip link set {{eth0}} down`

- 显示路由表：
  `ip route show`

- 添加默认网关：
  `sudo ip route add default via {{192.168.1.1}}`

- 添加 IP 地址：
  `sudo ip addr add {{192.168.1.100/24}} dev {{eth0}}`

- 删除 IP 地址：
  `sudo ip addr del {{192.168.1.100/24}} dev {{eth0}}`
