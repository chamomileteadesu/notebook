# tracepath

> 追踪到目的主机的路径，发现路径 MTU。
> 更多信息：<https://manned.org/tracepath>

- 追踪到主机的路径：
  `tracepath {{主机名}}`

- 追踪到指定端口：
  `tracepath -p {{端口}} {{主机名}}`

- 设置最大跳数：
  `tracepath -m {{跳数}} {{主机名}}`

- 设置初始端口：
  `tracepath -n {{起始端口}} {{主机名}}`

- 不解析主机名（显示 IP）：
  `tracepath -n {{主机名}}`

- 设置探测包的数量：
  `tracepath -b {{数量}} {{主机名}}`
