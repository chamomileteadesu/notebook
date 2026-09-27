# mount

> 挂载文件系统。  
> 更多信息：<https://manned.org/mount>

- 挂载设备到目录：

  `sudo mount /dev/sda1 /mnt/usb`

- 显示所有挂载点：

  `mount`

- 挂载指定类型的文件系统：

  `sudo mount -t ext4 /dev/sda1 /mnt`

- 重新挂载为读写模式：

  `sudo mount -o remount,rw /`

- 只读挂载：

  `sudo mount -o ro /dev/sda1 /mnt`

- 挂载 ISO 文件：

  `sudo mount -o loop 镜像.iso /mnt/iso`

- 显示特定文件系统类型的挂载：

  `mount -t ext4`
