# nix-collect-garbage

> 删除未被使用的 store 路径以释放空间。
> 更多信息：<https://nixos.org/manual/nix/stable/command-ref/nix-collect-garbage`

- 删除超过指定天数的旧生成：
  `sudo nix-collect-garbage --delete-older-than {{30d}}`

- 激进清理（删除所有历史生成，仅保留当前）：
  `sudo nix-collect-garbage -d`

- 删除所有未被引用的 store 路径：
  `nix-collect-garbage`

- 硬链接优化（去重）：
  `nix-store --optimise`

# nh clean

> nh 提供的更智能的清理工具。
> 更多信息：<https://github.com/viperML/nh>

- 根据保留生成的数量清理：
  `nh clean all --keep {{5}}`

- 清理指定用户配置：
  `nh clean user --keep {{3}}`

- 清理系统配置：
  `nh clean system --keep {{5}}`