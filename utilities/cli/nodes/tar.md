# tar

> 打包和解包工具，Linux 下最常用的归档工具。
> 更多信息：<https://manned.org/tar>

- 打包并压缩为 .tar.gz：
  `tar zcvf {{归档名.tar.gz}} {{目录}}`

- 解压 .tar.gz 文件：
  `tar zxvf {{归档名.tar.gz}}`

- 解压到指定目录：
  `tar zxvf {{归档名.tar.gz}} -C {{目标目录}}`

- 打包为 .tar.bz2：
  `tar jcvf {{归档名.tar.bz2}} {{目录}}`

- 解压 .tar.bz2 文件：
  `tar jxvf {{归档名.tar.bz2}}`

- 列出归档内容：
  `tar tvf {{归档名.tar.gz}}`

- 打包为 .tar.xz：
  `tar Jcvf {{归档名.tar.xz}} {{目录}}`

- 只打包特定文件：
  `tar zcvf {{归档名.tar.gz}} {{文件1}} {{文件2}}`
