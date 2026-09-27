# rg

> ripgrep - grep 的现代化替代品，极速的递归文本搜索工具。
> 更多信息：<https://github.com/BurntSushi/ripgrep>

- 递归搜索当前目录中的模式：
  `rg "{{模式}}"`

- 搜索指定目录：
  `rg "{{模式}}" {{路径}}`

- 忽略大小写
  `rg -i {{PATTERN}}`

- 严格匹配单词
  `rg -w {{PATTERN}}`

- 指定匹配后显示的行数（向下）
  `rg -A {{NUM}} {{PATTERN}}`

- 指定匹配后显示的行数（向上）
  `rg -B {{NUM}} {{PATTERN}}`

- 指定匹配后显示的行数（向上和向下）
  `rg -C {{NUM}} {{PATTERN}}`

- 搜索匹配模式的文件名：
  `rg --files | rg "{{模式}}"`

- 显示匹配行及上下文：
  `rg --context {{N}} "{{模式}}"`

- 只显示匹配的文件名：
  `rg --files-with-matches "{{模式}}"`

- 搜索隐藏文件和被忽略的文件：
  `rg --hidden --no-ignore "{{模式}}"`

- 按文件类型搜索：
  `rg --type {{py}} "{{模式}}"`

- 显示统计信息：
  `rg --stats "{{模式}}"`

- 替换匹配文本（不修改原文件）：
  `rg --replace "{{替换文本}}" "{{模式}}"`

- 使用正则表达式搜索：
  `rg -e "{{正则表达式}}"`
