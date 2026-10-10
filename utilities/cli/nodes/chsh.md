# chsh

> 更改用户登录 shell。
> 更多信息：<https://manned.org/chsh>

- 更改当前用户的登录 shell（交互式）：
  `chsh`

- 更改当前用户的登录 shell 为指定 shell：
  `chsh -s {{/bin/zsh}}`

- 更改指定用户的登录 shell：
  `sudo chsh -s {{/bin/zsh}} {{用户名}}`

- 列出可用的 shell：
  `chsh -l`

- 查看当前用户的 shell 信息：
  `chsh -p`