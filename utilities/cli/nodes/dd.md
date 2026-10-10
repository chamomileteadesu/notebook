# dd

> 转换并复制文件（常用于备份和创建启动盘）。
> 更多信息：<https://manned.org/dd>

- 从文件复制到文件：

  `dd if=源文件 of=目标文件`

- 创建可启动 U 盘：

  `sudo dd if=镜像.iso of=/dev/sdX bs=4M status=progress && sync`

- 创建指定大小的空文件：

  `dd if=/dev/zero of=文件 bs=1M count=大小MB`

- 备份整个磁盘：

  `sudo dd if=/dev/sda of=备份.img bs=4M status=progress`

- 从备份恢复磁盘：

  `sudo dd if=备份.img of=/dev/sda bs=4M status=progress`

- 擦除磁盘数据：

  `sudo dd if=/dev/zero of=/dev/sdX bs=4M status=progress`

- 显示复制进度（某些版本）：

  `dd if=源 of=目标 status=progress`

- 跳过输入文件的前 N 个块：

  `dd if=源文件 of=目标文件 skip=N`
