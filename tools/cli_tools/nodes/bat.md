# bat

> cat 的现代化替代品，支持语法高亮和 Git 集成的文件查看工具。
> 更多信息：<https://github.com/sharkdp/bat>

- 查看文件内容：
  `bat {{文件}}`

- 查看多个文件：
  `bat {{文件1}} {{文件2}}`

- 指定语法高亮语言：
  `bat --language {{python}} {{文件}}`

- 显示行号：
  `bat --number {{文件}}`

- 不显示 Git 修改标记：
  `bat --decorations=never {{文件}}`

- 输出无格式的纯文本（适合管道操作）：
  `bat --plain {{文件}}`

- 列出支持的语言：
  `bat --list-languages`

- 列出支持的主题：
  `bat --list-themes`

- 使用指定主题：
  `bat --theme {{TwoDark}} {{文件}}`
