# ss

> 转储套接字统计信息（比 netstat 更快更详细）。
> 更多信息：<https://manned.org/ss>

- 显示所有监听的 TCP 端口：

  `ss -tln`

- 显示所有监听的 TCP 和 UDP 端口：

  `ss -tuln`

- 显示所有连接的进程信息：
  `sudo ss -tulnp`

- 显示所有已建立的 TCP 连接：

  `ss -tn`

- 显示指定端口的连接：

  `ss -tn sport = :port`

- 显示指定目标端口的连接：

  `ss -tn dport = :port`

- 显示 TCP 连接状态：

  `ss -tan`

- 显示 UNIX 域套接字：

  `ss -xn`
