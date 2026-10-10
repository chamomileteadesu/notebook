# journalctl

> 查看 Systemd 日志。
> 更多信息：<https://manned.org/journalctl>

- 查看特定服务的日志：
  `journalctl -u {{服务名}}`

- 实时查看日志（跟随模式）：
  `journalctl -u {{服务名}} -f`

- 查看本次启动后的日志：
  `journalctl -b`

- 查看上一次启动的日志：
  `journalctl -b -1`

- 查看指定时间段的日志：
  `journalctl --since "{{2024-01-01}}" --until "{{2024-01-02}}"`

- 查看内核日志：
  `journalctl -k`

- 显示日志尾部（最后 N 条）：
  `journalctl -n {{N}}`

- 反向显示日志（从新到旧）：
  `journalctl -r`
