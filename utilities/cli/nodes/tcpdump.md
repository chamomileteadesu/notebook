# tcpdump

> 命令行网络数据包分析器。  
> 更多信息：<https://manned.org/tcpdump>

- 监听指定网络接口的所有流量：

  `sudo tcpdump -i eth0`

- 监听所有网络接口的流量：

  `sudo tcpdump -i any`

- 捕获指定数量的数据包后停止：

  `sudo tcpdump -c 数量`

- 捕获指定主机的流量：

  `sudo tcpdump host 192.168.1.1`

- 捕获指定端口的流量：

  `sudo tcpdump port 80`

- 捕获指定协议的流量（tcp/udp/icmp）：

  `sudo tcpdump tcp`

- 组合过滤条件（与、或、非）：

  `sudo tcpdump "tcp port 80 and host 192.168.1.1"`

- 将捕获的数据包保存到文件：

  `sudo tcpdump -w output.pcap`

- 从文件读取数据包进行分析：

  `sudo tcpdump -r output.pcap`

- 以详细和十六进制格式显示数据包内容：

  `sudo tcpdump -XX`
