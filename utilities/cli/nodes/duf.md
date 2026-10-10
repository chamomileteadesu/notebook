# duf

> df 的现代化替代品，更友好的磁盘使用情况查看工具。
> 更多信息：<https://github.com/muesli/duf>

- 显示所有磁盘使用情况：
  `duf`

- 显示指定目录或设备的磁盘使用情况：
  `duf {{路径}}`

- 显示所有文件系统（包括伪文件系统）：
  `duf --all`

- 只显示本地文件系统：
  `duf --only local`

- 只显示特定类型的文件系统：
  `duf --only-fs {{ext4,nfs}}`

- 按排序显示（如 size, used, avail, usage）：
  `duf --sort {{size}}`

- 输出 JSON 格式：
  `duf --json`

- 显示 inode 信息而非磁盘使用：
  `duf --inodes`
