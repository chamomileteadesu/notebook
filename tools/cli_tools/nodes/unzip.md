# unzip

> 解压 .zip 文件。
> 更多信息：<https://manned.org/unzip>

- 解压到当前目录：
  `unzip {{归档.zip}}`

- 解压到指定目录：
  `unzip {{归档.zip}} -d {{目录}}`

- 列出归档内容（不解压）：
  `unzip -l {{归档.zip}}`

- 解压时覆盖已存在的文件：
  `unzip -o {{归档.zip}}`

- 解压时不覆盖已存在的文件：
  `unzip -n {{归档.zip}}`

- 解压指定文件：
  `unzip {{归档.zip}} {{文件1}} {{文件2}}`

- 静默模式：
  `unzip -q {{归档.zip}}`
