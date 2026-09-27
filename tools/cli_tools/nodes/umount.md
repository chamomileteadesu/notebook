# umount

> 卸载文件系统。  
> 更多信息：<https://manned.org/umount>

- 卸载挂载点：

  `umount /mnt/usb`

- 卸载指定设备：

  `umount /dev/sda1`

- 强制卸载（设备忙时）：

  `umount -f 挂载点`

- 延迟卸载（等设备不忙时完成）：

  `umount -l 挂载点`

- 卸载所有挂载点：

  `umount -a`

- 显示详细信息：

  `umount -v 挂载点`
