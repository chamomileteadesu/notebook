# readlink

> 显示符号链接或规范文件名指向的目标。
> 更多信息：<https://manned.org/readlink>

- 查看符号链接指向的实际目标：
  `readlink {{路径/到/符号链接}}`

- 获取文件的绝对物理路径（解析所有父级符号链接）：
  `readlink -f {{路径/到/文件}}`
