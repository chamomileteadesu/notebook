# env

> 在修改后的环境中运行程序，或显示当前环境变量。
> 更多信息：<https://manned.org/env>

- 显示所有环境变量：
  `env`

- 临时设置变量并运行命令：
  `env {{VAR}}={{value}} {{命令}}`

- 从空环境开始运行命令：
  `env -i {{命令}}`

- 删除环境变量后运行命令：
  `env -u {{VAR}} {{命令}}`

- 设置多个变量：
  `env {{VAR1}}={{value1}} {{VAR2}}={{value2}} {{命令}}`

- 以指定路径作为 PATH 运行命令：
  `env PATH={{/custom/path}} {{命令}}`
