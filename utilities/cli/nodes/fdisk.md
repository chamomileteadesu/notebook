# fdisk

> 磁盘分区工具。
> 更多信息：<https://manned.org/fdisk>

- 列出所有分区表：
  `sudo fdisk -l`

- 列出指定设备的分区表：
  `sudo fdisk -l {{/dev/sda}}`

- 进入交互式分区界面：
  `sudo fdisk {{/dev/sda}}`

- 创建新分区（在交互模式中）：
  `n`

- 删除分区（在交互模式中）：
  `d`

- 打印分区表（在交互模式中）：
  `p`

- 写入更改并退出（在交互模式中）：
  `w`

- 不保存更改退出（在交互模式中）：
  `q`
