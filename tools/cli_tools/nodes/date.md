# date

> 显示或设置系统时间。
> 更多信息：<https://manned.org/date>

- 显示当前系统时间：
  `date`

- 以 UTC 时间显示：
  `date -u`

- 按指定格式显示时间：
  `date "+%Y-%m-%d %H:%M:%S"`

- 显示昨天日期：
  `date -d "yesterday"`

- 显示指定日期：
  `date -d "2024-01-01"`

- 计算相对日期：
  `date -d "next monday"`
  `date -d "2 weeks ago"`

- 设置系统时间（需要 root）：
  `sudo date -s "2024-01-01 12:00:00"`

- 显示 Unix 时间戳：
  `date +%s`

- 从 Unix 时间戳转换为可读时间：
  `date -d @{{时间戳}}`
