# printenv

> 打印全部或指定的环境变量值。
> 更多信息：<https://manned.org/printenv>

- 打印所有环境变量：
  `printenv`

- 打印指定环境变量的值：
  `printenv {{HOME}}`

- 打印多个环境变量的值：
  `printenv {{HOME}} {{PATH}} {{USER}}`

- 打印 PATH 环境变量：
  `printenv PATH`

- 在脚本中使用（输出可被捕获）：
  `VAR=$(printenv {{变量名}})`
