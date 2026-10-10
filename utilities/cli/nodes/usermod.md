# usermod

> 修改用户账户。
> 更多信息：<https://manned.org/usermod>

- 将用户添加到附加组：
  `sudo usermod -aG {{组名}} {{用户名}}`

- 修改用户的默认 Shell：
  `sudo usermod -s {{/bin/zsh}} {{用户名}}`

- 修改用户的主目录：
  `sudo usermod -d {{/home/新目录}} {{用户名}}`

- 修改用户的登录名：
  `sudo usermod -l {{新用户名}} {{旧用户名}}`

- 锁定用户账户：
  `sudo usermod -L {{用户名}}`

- 解锁用户账户：
  `sudo usermod -U {{用户名}}`

- 修改用户的主组：
  `sudo usermod -g {{组名}} {{用户名}}`
