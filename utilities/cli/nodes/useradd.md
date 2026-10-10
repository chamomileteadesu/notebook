# useradd

> 创建新用户。
> 更多信息：<https://manned.org/useradd>

- 创建用户：
  `sudo useradd {{用户名}}`

- 创建用户并创建主目录：
  `sudo useradd -m {{用户名}}`

- 创建用户并指定默认 Shell：
  `sudo useradd -s {{/bin/bash}} {{用户名}}`

- 创建用户并指定主目录：
  `sudo useradd -m -d {{/home/目录}} {{用户名}}`

- 创建用户并指定用户组：
  `sudo useradd -g {{组名}} {{用户名}}`

- 创建用户并指定附加组：
  `sudo useradd -G {{组1,组2}} {{用户名}}`

- 创建系统用户：
  `sudo useradd -r {{用户名}}`
