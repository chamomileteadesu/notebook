# nix-env (Legacy)

> 旧版 Nix 包管理工具，不支持 Flakes，推荐使用 `nix profile`。
> 更多信息：<https://nixos.org/manual/nix/stable/command-ref/nix-env>

- 安装包（旧版语法）：
  `nix-env -iA nixpkgs.{{包名}}`

- 卸载包：
  `nix-env -e {{包名}}`

- 列出已安装的包：
  `nix-env -q`

- 查询可用包：
  `nix-env -qaP {{包名}}`

- 更新包：
  `nix-env -u {{包名}}`

- 回滚到上一代配置：
  `nix-env --rollback`

- 列出所有代：
  `nix-env --list-generations`

# nix profile

> 现代 Nix 包管理工具（Flakes）。
> 更多信息：<https://nixos.org/manual/nix/stable/command-ref/new-cli/nix3-profile`

- 安装包：
  `nix profile install nixpkgs#{{包名}}`

- 列出已安装内容：
  `nix profile list`

- 更新所有包：
  `nix profile upgrade --all`

- 卸载包：
  `nix profile remove {{索引或ID}}`

- 移除旧配置代：
  `nix profile wipe-history --older-than {{30d}}`
