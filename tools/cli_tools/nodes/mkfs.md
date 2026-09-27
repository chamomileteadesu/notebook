# mkfs

> 创建文件系统（格式化分区）。
> 更多信息：<https://manned.org/mkfs>

- 格式化为 ext4：
  `sudo mkfs.ext4 {{/dev/sda1}}`

- 格式化为 ext3：
  `sudo mkfs.ext3 {{/dev/sda1}}`

- 格式化为 xfs：
  `sudo mkfs.xfs {{/dev/sda1}}`

- 格式化为 vfat（FAT32）：
  `sudo mkfs.vfat {{/dev/sdb1}}`

- 格式化为 btrfs：
  `sudo mkfs.btrfs {{/dev/sda1}}`

- 指定卷标：
  `sudo mkfs.ext4 -L {{卷标}} {{/dev/sda1}}`
