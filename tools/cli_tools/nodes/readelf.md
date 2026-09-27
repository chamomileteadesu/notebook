# readelf

> 显示 ELF（Executable and Linkable Format）文件的信息。
> 更多信息：<https://manned.org/readelf>

- 查看文件头信息：
  `readelf -h {{文件名}}`

- 查看所有信息：
  `readelf -a {{文件名}}`

- 查看段头表（Program Headers）：
  `readelf -l {{文件名}}`

- 查看节头表（Section Headers）：
  `readelf -S {{文件名}}`

- 查看符号表（Symbols）：
  `readelf -s {{文件名}}`
