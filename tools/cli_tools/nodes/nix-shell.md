# nix-shell (Legacy)

> 旧版临时环境工具。推荐使用 `nix shell` 或 `nix develop`。
> 更多信息：<https://nixos.org/manual/nix/stable/command-ref/nix-shell`

- 进入包含指定包的环境：
  `nix-shell -p {{包名}}`

- 运行命令并退出：
  `nix-shell -p {{包名}} --run "{{命令}}"`

- 从表达式文件启动：
  `nix-shell -p {{包名1}} {{包名2}}`

- 使用 shell.nix 定义的环境：
  `nix-shell`

# nix shell

> 临时使用包（Flakes）。
> 更多信息：<https://nixos.org/manual/nix/stable/command-ref/new-cli/nix3-shell`

- 启动包含指定包的 shell：
  `nix shell nixpkgs#{{包名1}} nixpkgs#{{包名2}}`

- 直接运行命令：
  `nix shell nixpkgs#{{包名}} -c {{命令}}`

# nix develop

> 进入项目开发环境（Flakes）。
> 更多信息：<https://nixos.org/manual/nix/stable/command-ref/new-cli/nix3-develop`

- 使用当前目录 flake.nix 的 devShell：
  `nix develop`

- 使用指定 flake 的 devShell：
  `nix develop {{flake路径}}#{{devShell名}}`

- 运行命令并退出：
  `nix develop -c {{命令}}`

# nix run

> 不进入 shell 直接运行包中的程序。
> 更多信息：<https://nixos.org/manual/nix/stable/command-ref/new-cli/nix3-run`

- 运行包的默认程序：
  `nix run nixpkgs#{{包名}}`

- 运行并传递参数：
  `nix run nixpkgs#{{包名}} -- {{参数}}`