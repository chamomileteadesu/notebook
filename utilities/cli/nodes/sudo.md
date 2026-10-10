# sudo

> 以其他用户（默认 root）的身份执行命令。
> 更多信息：<https://manned.org/sudo>

- 以 root 身份运行命令：
  `sudo {{命令}}`

- 以指定用户身份运行命令：
  `sudo -u {{用户名}} {{命令}}`

- 切换到 root shell：
  `sudo -i`

- 以 root 身份启动登录 shell：
  `sudo -s`

- 列出当前用户可执行的 sudo 命令：
  `sudo -l`

- 验证 sudo 会话（延长超时时间）：
  `sudo -v`

- 编辑文件（使用默认编辑器）：
  `sudo -e {{/etc/hosts}}`

- 保留环境变量运行命令：
  `sudo -E {{命令}}`
