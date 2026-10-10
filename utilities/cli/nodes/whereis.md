# whereis

> 查找命令的二进制文件、源码和手册页位置。
> 更多信息：<https://manned.org/whereis>

- 查找命令的二进制文件、源码和手册页：
  `whereis {{命令}}`

- 只查找二进制文件：
  `whereis -b {{命令}}`

- 只查找手册页：
  `whereis -m {{命令}}`

- 只查找源码文件：
  `whereis -s {{命令}}`

- 查找多个命令：
  `whereis {{命令1}} {{命令2}}`

- 在指定路径中搜索：
  `whereis -B {{/usr/bin}} -f {{命令}}`
