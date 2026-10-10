# hostnamectl

> 查询和更改系统主机名及相关设置。
> 更多信息：<https://manned.org/hostnamectl>

- 显示当前主机名和相关信息：
  `hostnamectl`

- 设置主机名：
  `hostnamectl set-hostname {{主机名}}`

- 设置静态主机名（永久保存）：
  `hostnamectl set-hostname {{主机名}} --static`

- 设置漂亮主机名（可包含特殊字符）：
  `hostnamectl set-hostname "{{My Computer}}" --pretty`

- 设置主机图标名称：
  `hostnamectl set-icon-name {{图标名}}`

- 设置机箱类型（如 desktop、laptop、server）：
  `hostnamectl set-chassis {{类型}}`

- 清除主机名恢复默认：
  `hostnamectl set-hostname ""`