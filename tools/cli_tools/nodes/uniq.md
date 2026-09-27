# uniq

> 报告或省略重复的行（通常配合 sort 使用）。
> 更多信息：<https://manned.org/uniq>

- 去除相邻重复行：
  `sort {{文件}} | uniq`

- 统计每行出现的次数：
  `sort {{文件}} | uniq -c`

- 只显示重复的行：
  `sort {{文件}} | uniq -d`

- 只显示不重复的行：
  `sort {{文件}} | uniq -u`

- 忽略前 N 个字段：
  `sort {{文件}} | uniq -f {{N}}`

- 忽略大小写：
  `sort {{文件}} | uniq -i`
