# nh

> Nix Helper，提供更简洁的 NixOS 命令行体验。
> 更多信息：<https://github.com/viperML/nh>

- 系统切换（自动寻找当前目录的 flake.nix，并根据当前 hostname 进行构建）：
  `nh os switch .`

- 垃圾回收（保留最近 N 个生成）：
  `nh clean all --keep {{5}}`

- 搜索包：
  `nh search {{包名}}`

- 更新 flake 输入并切换：
  `nh os switch . --update`

- 生成并应用 home-manager 配置：
  `nh home switch .`

- 查看构建差异：
  `nh os switch . --diff`
