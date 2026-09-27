# nix-store

> 操作 Nix Store。
> 更多信息：<https://nixos.org/manual/nix/stable/command-ref/nix-store>

- 验证 Store 完整性：
  `nix-store --verify --check-contents`

- 优化 Store（硬链接去重）：
  `nix-store --optimise`

- 查询包的依赖：
  `nix-store --query --references {{/nix/store/...}}`

- 查询包的反向依赖：
  `nix-store --query --referrers {{/nix/store/...}}`

- 列出包的所有输出：
  `nix-store --query --outputs {{/nix/store/...}}`
