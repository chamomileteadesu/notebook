# bzip2

> 压缩或解压文件（.bz2），压缩率通常比 gzip 高。
> 更多信息：<https://manned.org/bzip2>

- 压缩文件：
  `bzip2 path/to/file`

- 解压文件：
  `bzip2 -d path/to/file.bz2`

- 压缩文件并保留原文件：
  `bzip2 -k path/to/file`

- 设置压缩级别（1-9）：
  `bzip2 [-level] path/to/file`

- 测试压缩文件完整性：
  `bzip2 -t path/to/file.bz2`
