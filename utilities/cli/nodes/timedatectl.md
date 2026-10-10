# timedatectl

> 查询和更改系统时间和日期设置。
> 更多信息：<https://manned.org/timedatectl>

- 显示当前时间和日期设置：
  `timedatectl`

- 列出所有可用时区：
  `timedatectl list-timezones`

- 设置时区：
  `timedatectl set-timezone {{Asia/Shanghai}}`

- 启用 NTP 时间同步：
  `timedatectl set-ntp true`

- 禁用 NTP 时间同步：
  `timedatectl set-ntp false`

- 手动设置时间：
  `timedatectl set-time "{{2024-01-01 12:00:00}}"`

- 仅设置日期：
  `timedatectl set-time "{{2024-01-01}}"`

- 设置本地 RTC 时间模式：
  `timedatectl set-local-rtc true`

- 查看 NTP 同步状态：
  `timedatectl timesync-status`

- 显示详细的 NTP 服务器信息：
  `timedatectl show-timesync`
