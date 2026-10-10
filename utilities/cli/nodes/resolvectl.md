# resolvectl

> 查询和控制在 systemd-resolved 中的 DNS 解析。
> 更多信息：<https://manned.org/resolvectl>

- 显示当前 DNS 配置：
  `resolvectl status`

- 查询域名解析：
  `resolvectl query {{域名}}`

- 查询指定类型的 DNS 记录：
  `resolvectl query -t {{A}} {{域名}}`

- 查询 MX 记录：
  `resolvectl query -t MX {{域名}}`

- 反向 DNS 查询（IP 到域名）：
  `resolvectl query {{IP地址}}`

- 设置指定接口的 DNS 服务器：
  `resolvectl dns {{接口名}} {{DNS服务器IP}}`

- 设置全局 DNS 服务器：
  `resolvectl dns {{DNS服务器IP}}`

- 清除 DNS 缓存：
  `resolvectl flush-caches`

- 显示 DNS 缓存统计：
  `resolvectl statistics`

- 设置搜索域：
  `resolvectl domain {{接口名}} {{搜索域}}`

- 启用/禁用 DNSSEC：
  `resolvectl dnssec {{接口名}} {{true|false}}`

- 设置备用 DNS 服务器：
  `resolvectl fallback-dns {{DNS服务器IP}}`

- 重置接口的 DNS 配置：
  `resolvectl revert {{接口名}}`
