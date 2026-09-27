# dmesg

> 显示内核环形缓冲区的信息（通常用于硬件故障诊断）。
> 更多信息：<https://manned.org/dmesg>

- 显示所有内核消息：
  `dmesg`

- 搜索包含特定关键字的消息：
  `dmesg | grep -i "{{error}}"`

- 以人类可读的时间戳显示：
  `dmesg -T`

- 只显示错误级别的消息：
  `dmesg -l err`

- 实时监控内核消息：
  `dmesg -w`

- 清空内核环形缓冲区：
  `sudo dmesg -c`

- 显示最后 N 条消息：
  `dmesg | tail -n {{N}}`
