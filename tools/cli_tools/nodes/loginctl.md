# loginctl

> 管理登录会话和用户。
> 更多信息：<https://manned.org/loginctl>

- 列出所有会话：
  `loginctl list-sessions`

- 显示当前会话详情：
  `loginctl`

- 显示指定会话详情：
  `loginctl show-session {{会话ID}}`

- 列出所有登录用户：
  `loginctl list-users`

- 显示指定用户详情：
  `loginctl show-user {{用户名}}`

- 显示当前会话的用户：
  `loginctl user-status`

- 显示指定用户的会话状态：
  `loginctl user-status {{用户名}}`

- 终止指定会话：
  `loginctl terminate-session {{会话ID}}`

- 终止指定用户的所有会话：
  `loginctl terminate-user {{用户名}}`

- 锁定当前会话：
  `loginctl lock-session`

- 锁定所有会话：
  `loginctl lock-sessions`

- 解锁所有会话：
  `loginctl unlock-sessions`

- 强制用户注销：
  `loginctl kill-user {{用户名}}`
