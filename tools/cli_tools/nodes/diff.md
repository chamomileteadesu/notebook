# diff

> 比较文件差异，生成补丁文件。
> 更多信息：<https://manned.org/diff>

- 比较两个文件：

  `diff file1 file2`

- 以统一格式输出（更易读，更常用）：

  `diff [-u|--unified] file1 file2`

- 显示为左右两栏：

  `diff [-y|--size-by-size] file1 file2`

- 递归比较目录：

  `diff [-r|--recursive] dir1 dir2`

- 忽略空格差异：

  `diff [-w|--ignore-all-space] file1 file2`

- 忽略大小写差异：

  `diff [-i|ignore-case] file1 file2`

- 生成补丁文件：

  `diff [-u|--unified] file1 file2 > patch_file`

- 显示差异所在的函数：

  `diff [-p|--show-c-function] file1 file2`
