# lsblk

> 列出块设备信息。
> 更多信息：<https://manned.org/lsblk>

- 列出所有块设备：
  `lsblk`

- 显示文件系统信息（UUID、类型等）：
  `lsblk -f`

- 显示设备大小以字节为单位：
  `lsblk -b`

- 输出 JSON 格式：
  `lsblk -J`

- 显示完整设备路径：
  `lsblk -p`

- 显示设备所有者、组和权限：
  `lsblk -m`

- 只显示指定设备的信息：
  `lsblk {{/dev/sda}}`

- 显示设备拓扑信息：
  `lsblk -t`
