# nix flake

> 管理 Nix Flakes 的核心命令。
> 更多信息：<https://nixos.org/manual/nix/stable/command-ref/new-cli/nix3-flake>

- 更新所有输入并锁定：
  `nix flake update`

- 仅更新特定输入：
  `nix flake lock --update-input {{输入名}}`

- 检查 Flake 语法与构建：
  `nix flake check`

- 显示 Flake 的输出结构：
  `nix flake show`

- 初始化新 Flake：
  `nix flake init`

- 使用模板初始化 Flake：
  `nix flake init -t {{模板名}}`

- 查看 Flake 元数据：
  `nix flake metadata`

- 添加新输入到 Flake：
  `nix flake lock --update-input {{输入名}}`
