# history

> 显示或操作历史命令列表。
> 更多信息：<https://manned.org/history>

- 显示历史命令：
  `history`

- 显示最近 N 条历史命令：
  `history {{N}}`

- 清空历史记录：
  `history -c`

- 从文件恢复历史记录：
  `history -r {{文件名}}`

- 将历史记录写入文件：
  `history -w {{文件名}}`

- 删除指定行的历史：
  `history -d {{行号}}`

- 执行上 1000 条命令
  `!1000`
- 执行上一条命令

- 相关环境变量

  ```sh
  # 查看历史命令记录最大数目
  echo $HISTSIZE
  # 查看历史命令记录文件路径
  echo $HISTFILE
  ```
