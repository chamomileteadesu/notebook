# dirname

> 从路径中提取目录名。
> 更多信息：<https://manned.org/dirname>

- 提取目录路径：
  `dirname {{/path/to/file}}`

- 提取多个路径的目录名：
  `dirname {{/path/to/file1}} {{/path/to/file2}}`

- 处理以斜杠结尾的路径：
  `dirname {{/path/to/dir/}}`

- 支持零字节分隔的输入：
  `dirname -z {{/path/to/file}}`
