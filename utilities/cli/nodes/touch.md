# touch

> 创建空文件或更改文件的访问/修改时间戳。
> 更多信息：<https://manned.org/touch>

- 创建一个新文件或更新现有文件的时间戳：
  `touch {{文件名}}`

- 如果文件不存在，则不创建新文件：
  `touch --no-create {{文件名}}`

- 将文件的时间戳设置为特定日期和时间：
  `touch -t {{YYYYMMDDHHMM.SS}} {{文件名}}`

- 使用另一个文件的时间戳来设置当前文件：
  `touch -r {{参照文件}} {{目标文件}}`

- 使用人类可读的格式指定时间

  ```shell
    touch -d "2025-12-31 23:59:59" report.txt
    touch -d "yesterday" oldfile.txt
    touch -d "2 days ago" test.log
    touch -d "next monday" future.txt
  ```

- 只修改 atime
  `touch -a --no-create {{file_name}}`

- 只修改 mtime
  `touch -m --no-create {{file_name}}`
