# passwd

> 更新用户认证令牌（修改密码）。
> 更多信息：<https://manned.org/passwd>

- 修改当前用户密码：
  `passwd`

- 修改指定用户密码（需要 root）：
  `sudo passwd {{用户名}}`

- 锁定用户账户：
  `sudo passwd -l {{用户名}}`

- 解锁用户账户：
  `sudo passwd -u {{用户名}}`

- 使密码立即过期：
  `sudo passwd -e {{用户名}}`

- 删除用户密码：
  `sudo passwd -d {{用户名}}`

- 显示用户密码状态：
  `sudo passwd -S {{用户名}}`
