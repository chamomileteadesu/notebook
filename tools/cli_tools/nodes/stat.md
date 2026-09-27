# stat

> 显示文件或文件系统的状态信息。  
> See alse: [[file]].  
> 更多信息：<https://manned.org/stat>

- 显示文件状态：

  `stat path/to/file`

- 显示文件系统状态而非文件状态：

  `stat [-f|--file-system] path/to/file`

- 不显示标签，以简洁格式输出：

  `stat [-t|--terse] path/to/file`

- 使用指定格式显示：

  `stat [-c|--format] "%n: %s bytes" path/to/file`

- 显示常用格式（权限、大小、修改时间）：

  `stat [-c|--format] "%A %s %y %n" path/to/file`

- 显示文件的 inode 号：

  `stat [-c|--format] "%i" path/to/file`
