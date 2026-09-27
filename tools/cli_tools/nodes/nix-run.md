# nix run

> 直接构建并运行包中的默认可执行程序。
> 更多信息：<https://nixos.org/manual/nix/stable/command-ref/new-cli/nix3-run`

- 运行 nixpkgs 中的包：
  `nix run nixpkgs#{{包名}}`

- 运行特定版本的包：
  `nix run github:nixos/nixpkgs/{{分支}}#{{包名}} -- {{参数}}`

- 运行当前 Flake 的 defaultPackage：
  `nix run .`

- 运行远程 Flake：
  `nix run {{github:用户/仓库}}#{{包名}}`

- 运行并传递参数：
  `nix run nixpkgs#{{包名}} -- {{参数1}} {{参数2}}`