# unset

> 删除 shell 变量或函数。
> 更多信息：<https://manned.org/unset>

- 删除变量：
  `unset {{变量名}}`

- 删除多个变量：
  `unset {{变量1}} {{变量2}}`

- 删除函数：
  `unset -f {{函数名}}`

- 删除只读变量（某些 shell 不支持）：
  `unset -v {{变量名}}`
