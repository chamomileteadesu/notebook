# basename

> 从路径中提取文件名。
> 更多信息：<https://manned.org/basename>

- 提取文件名：
  `basename {{/path/to/file}}`

- 移除指定后缀：
  `basename {{/path/to/file.txt}} .txt`

- 提取多个路径的文件名：
  `basename -a {{/path/to/file1}} {{/path/to/file2}}`

- 处理带后缀的多个文件：
  `basename -a -s .txt {{/path/to/file1.txt}} {{/path/to/file2.txt}}`

- 不处理空参数：
  `basename -- {{路径}}`
