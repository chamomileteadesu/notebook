# nixos-option

> 查询 NixOS 配置选项的状态及其定义位置。
> 更多信息：<https://nixos.org/manual/nixos/stable/#sec-nixos-option`

- 查询某个选项的当前值：
  `nixos-option {{选项路径}}`

- 查询包含子选项的配置组：
  `nixos-option {{配置组名}}`

- 显示选项的定义位置：
  `nixos-option --value {{选项路径}}`