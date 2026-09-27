# nix search

> 在 Flake 中搜索包。
> 更多信息：<https://nixos.org/manual/nix/stable/command-ref/new-cli/nix3-search>

- 在 nixpkgs 中搜索包：
  `nix search nixpkgs {{包名}}`

- 使用正则表达式搜索：
  `nix search nixpkgs {{正则表达式}}`

- 搜索指定 flake：
  `nix search {{flake路径}} {{包名}}`

- 显示包的详细信息：
  `nix search nixpkgs {{包名}} --json`