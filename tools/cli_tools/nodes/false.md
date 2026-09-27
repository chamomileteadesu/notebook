# false

> 返回失败退出码（1）。
> 更多信息：<https://manned.org/false>

- 返回失败退出码：
  `false`

- 在条件语句中使用：
  `if false; then {{echo "不会执行"}}; fi`

- 检查退出码：
  `false; echo $?`

- 在逻辑与/或中使用：
  `true && false; echo $?`