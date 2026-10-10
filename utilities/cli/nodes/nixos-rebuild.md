# nixos-rebuild

> NixOS 系统重构工具，用于应用配置更改。
> 更多信息：<https://nixos.org/manual/nixos/stable/#sec-nixos-rebuild>

- 使用 Flake 应用配置：
  `sudo nixos-rebuild switch --flake .#{{主机名}}`

- 仅构建不切换（测试配置）：
  `sudo nixos-rebuild test --flake .#{{主机名}}`

- 构建并设置作为下次启动项：
  `sudo nixos-rebuild boot --flake .#{{主机名}}`

- 构建但不做任何更改：
  `sudo nixos-rebuild build --flake .#{{主机名}}`

- 列出可用的系统生成：
  `nixos-rebuild list-generations`