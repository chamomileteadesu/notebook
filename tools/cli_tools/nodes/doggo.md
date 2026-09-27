# dog

> dig 的现代化替代品，更友好的 DNS 查询工具。  
> 更多信息：<https://github.com/ogham/dog#examples>

- 查詢域名的記錄：

  `dog domain`

- 查询特定类型的 DNS 记录（如 A, AAAA, MX, NS, TXT）：

  `dog domain MX`

- 指定 DNS 服务器：

  `dog domain @8.8.8.8`

- 使用 JSON 格式输出：

  `dog domain --json`

- 显示详细的 DNS 响应：

  `dog domain --time`

- 反向 DNS 查询（IP 到 domain）：

  `dog -x IP地址`

- 查询所有类型的记录：

  `dog domain ANY`

- 使用 DoH:

  `dog domain -H|--https https://cloudflare-dns.com/dns-query`
