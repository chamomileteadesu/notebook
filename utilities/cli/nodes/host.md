# host

> DNS 查询工具，用于查找域名对应的 IP 地址或反向查询。
> 更多信息：<https://manned.org/host>

- 查询域名的 IP 地址：
  `host {{域名}}`

- 反向查询 IP 对应的域名：
  `host {{IP地址}}`

- 查询指定类型的 DNS 记录：
  `host -t {{MX}} {{域名}}`

- 指定 DNS 服务器：
  `host {{域名}} {{8.8.8.8}}`

- 显示详细信息：
  `host -v {{域名}}`

- 查询所有类型的 DNS 记录：
  `host -t ANY {{域名}}`
