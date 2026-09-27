# awk

> 强大的文本处理工具，用于模式扫描和处理语言。  
> awk 語法：[[languages/domain_specific_languages/awk/index]]。  
> 更多信息：<https://manned.org/awk>

- 打印每行的第 1、3 列：
  `awk '{ print $1, $3 }' {{文件}}`

- 指定分隔符为冒号：
  `awk -F ":" '{ print $1 }' {{文件}}`

- 打印包含指定模式的行：
  `awk '/{{模式}}/ { print }' {{文件}}`

- 打印第 3 列大于 100 的行：
  `awk '$3 > 100 { print }' {{文件}}`

- 使用 BEGIN 和 END 进行统计：
  `awk 'BEGIN { sum=0 } { sum+=$1 } END { print sum }' {{文件}}`

- 计算文件行数：
  `awk 'END { print NR }' {{文件}}`

- 打印最后一列：
  `awk '{ print $NF }' {{文件}}`

- 格式化输出：
  `awk '{ printf "%-10s %s\n", $1, $2 }' {{文件}}`
