# ping

> 向网络主机发送 ICMP ECHO_REQUEST 数据包。  
> 更多信息：<https://manned.org/ping>

- 指定主机：

  `ping host`

- 限制发送包的数量：

  `ping -c 次数 host`

- 设置发送间隔（秒）：

  `ping -i 秒数 host`

- 设置超时时间：

  `ping -W 秒数 host`

- 持续 ping 直到中断（Ctrl+C）：

  `ping host`

- 设置发送包的大小：

  `ping -s 字节数 host`

- 洪水式 ping（快速发送）：

  `ping -f host`

- 设置 TTL（生存时间）值：

  `ping -t TTL值 host`
