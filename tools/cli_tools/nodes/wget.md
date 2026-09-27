# wget

> 非交互式网络下载器。
> 更多信息：<https://manned.org/wget>

- 下载文件：
  `wget {{URL}}`

- 下载文件并指定输出文件名：
  `wget -O {{文件名}} {{URL}}`

- 断点续传：
  `wget -c {{URL}}`

- 后台下载：
  `wget -b {{URL}}`

- 递归下载整个网站：
  `wget -r {{URL}}`

- 限速下载：
  `wget --limit-rate={{1M}} {{URL}}`

- 静默模式（不显示进度）：
  `wget -q {{URL}}`

- 跳过 SSL 证书验证：
  `wget --no-check-certificate {{URL}}`
