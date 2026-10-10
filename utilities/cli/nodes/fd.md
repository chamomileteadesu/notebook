# fd

> find 的现代化替代品，更快速、更友好的文件搜索工具。  
> 更多信息：<https://github.com/sharkdp/fd>

- 递归搜索当前目录中匹配模式的文件：

  `fd "pattern"`

- 搜索指定目录：

  `fd "pattern" path`

- 搜索文件名并执行命令：

  `fd "pattern" [-x|--exec] command`

- 按扩展名搜索：

  `fd [-e|--extension] txt`

- 搜索隐藏文件和被忽略的文件：

  `fd [-H|--hidden] [-I|--no-ignore] "pattern"`

- 只搜索目录：

  `fd --type directory "pattern"`

- 搜索并排除某些目录：

  `fd [-E|--exclude] node_modules "pattern"`

- Find files only in the current directory:

  `fd [-d|--max-depth] 1 "pattern"`
