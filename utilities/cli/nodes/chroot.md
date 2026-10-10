# chroot

> 在新的根目录下运行命令或交互式 shell。
> 更多信息：<https://manned.org/chroot>

- 以指定目录作为新的根目录运行命令：
  `chroot {{/path/to/new/root}} {{命令}}`

- 以指定目录作为新的根目录启动交互式 shell：
  `chroot {{/path/to/new/root}} /bin/sh`

- 指定用户和组运行命令：
  `chroot --userspec={{用户}}:{{组}} {{/path/to/new/root}} {{命令}}`

- 指定补充组运行命令：
  `chroot --groups={{组1}},{{组2}} {{/path/to/new/root}} {{命令}}`

- 跳过 chroot 目录的权限检查：
  `chroot --skip-chdir {{/path/to/new/root}} {{命令}}`
