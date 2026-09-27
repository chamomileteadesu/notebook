# gzip

> 压缩或解压文件（.gz 格式）。
> 更多信息：<https://manned.org/gzip>

- 压缩文件（原文件会被替换）：
  `gzip path/to/file`

- 解压文件：
  `gzip -d path/to/file.gz`

- 压缩文件并保留原文件：
  `gzip -k path/to/file`

- 压缩文件并显示压缩进度：
  `gzip -v path/to/file`

- 指定压缩级别（1-9，默认 6）：
  `gzip -9 path/to/file`

- 递归压缩目录中的所有文件：
  `gzip -r path/to/dir`

- 测试压缩文件完整性：
  `gzip -tv path/to/file.gz`

- 查看压缩文件内容（不解压）：
  `zcat path/to/file.gz`
