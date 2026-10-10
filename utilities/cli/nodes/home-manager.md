# home-manager

> 用户个人环境管理工具（Dotfiles 管理）。
> 更多信息：<https://github.com/nix-community/home-manager>

- 应用配置更改：
  `home-manager switch --flake .#{{用户名}}`

- 查看当前生成：
  `home-manager generations`

- 删除超过指定天数的旧生成：
  `home-manager expire-generations "{{-30 days}}"`

- 切换到特定生成：
  `/nix/store/...-home-manager-generation-{{id}}/activate`

- 编辑配置：
  `home-manager edit`

- 构建但不应用：
  `home-manager build --flake .#{{用户名}}`

# nh home

> nh 提供的 home-manager 快捷命令。
> 更多信息：<https://github.com/viperML/nh>

- 自动识别 flake 并应用配置：
  `nh home switch .`

- 指定配置名应用：
  `nh home switch . -- {{用户名}}`