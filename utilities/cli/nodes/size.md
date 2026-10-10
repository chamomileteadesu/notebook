# size

> 显示目标文件或可执行文件的段大小信息。
> 更多信息：<https://manned.org/size>

- 显示文件的默认段大小：
  `size {{目标文件}}`

- 以十进制格式显示大小：
  `size -d {{目标文件}}`

- 以八进制格式显示大小：
  `size -o {{目标文件}}`

- 以十六进制格式显示大小：
  `size -x {{目标文件}}`

- 显示所有段的大小：
  `size -A {{目标文件}}`

- 显示 Berkeley 格式的段大小：
  `size -B {{目标文件}}`

- 显示可执行文件的段大小：
  `size {{可执行文件}}`

- 显示目标文件的段大小：
  `size {{目标文件}}`

- 显示共享库的段大小：
  `size {{共享库.so}}`

- 比较两个文件的大小：
  `size {{文件1}} {{文件2}}`

- 显示多个文件的总大小：
  `size *.o`

- 显示文件的大小并排序：
  `size *.o | sort -k3 -nr`

- 显示特定目录中所有目标文件的大小：
  `size {{目录}}/*.o`

- 显示文件的大小并统计总和：
  `size *.o | tail -1`

- 显示文件的大小并过滤特定段：
  `size -A {{目标文件}} | grep -E "(text|data|bss)"`

- 显示文件的段大小百分比：
  `size -A {{目标文件}} | awk 'NR>1 && $2!="" {printf "%s: %.2f%%\n", $1, $2/total*100} END{print "Total:", total}'`

- 显示静态库成员的大小：
  `size {{静态库.a}}`

- 显示文件的段大小详细信息：
  `size -A -d {{目标文件}}`

- 比较优化前后的文件大小：
  `size {{原始文件}} {{优化文件}}`

- 显示内核模块的大小：
  `size {{内核模块.ko}}`

- 显示文件的段大小并计算代码密度：
  `size -A {{目标文件}} | awk '/\.text/ {text=$2} /\.data/ {data=$2} /\.bss/ {bss=$2} END{total=text+data+bss; printf "Text: %d (%.2f%%)\nData: %d (%.2f%%)\nBSS: %d (%.2f%%)\nTotal: %d\n", text, text/total*100, data, data/total*100, bss, bss/total*100, total}'`

- 显示所有段的大小包括调试信息：
  `size -A {{目标文件}} | grep -v "\.debug"`

- 显示文件的大小并按类型分类：
  `size -A {{目标文件}} | awk 'NR>1 {if($2 ~ /^[0-9]+/) sum+=$2} END{print "Total size:", sum}'`

- 显示文件的段大小并生成报告：
  `size -A {{目标文件}} > {{大小报告文件}}`

- 显示动态库的段大小：
  `size -d {{动态库.so}}`

- 比较不同编译选项的文件大小：
  `size {{文件_O0}} {{文件_O2}} {{文件_O3}}`

- 显示文件的段大小并检查内存对齐：
  `size -A {{目标文件}} | awk '{print $1, $2, $3}'`

- 显示文件的大小并分析优化效果：
  `size {{优化前}} {{优化后}} | awk 'NR==1{opt1=$3} NR==2{opt2=$3} END{printf "Optimization reduced size by %d bytes (%.2f%%)\n", opt1-opt2, (opt1-opt2)/opt1*100}'`

- 显示静态链接和动态链接文件的大小差异：
  `size {{静态可执行文件}} {{动态可执行文件}}`

- 显示文件的段大小并计算内存占用：
  `size -A {{目标文件}} | awk '/\.text/ {text=$2} /\.data/ {data=$2} /\.bss/ {bss=$2} END{print "Runtime memory:", text+data+bss, "bytes"}'`

- 显示所有目标文件的大小统计：
  `for file in *.o; do echo "=== $file ==="; size -A $file; done`

- 显示文件的段大小并检查符号表影响：
  `size {{目标文件}} {{目标文件_stripped}}`

- 显示文件的段大小并分析代码段比例：
  `size -A {{目标文件}} | awk '/\.text/ {text=$2} END{print "Code segment percentage:", text/$2*100, "%"}'`

- 显示不同架构的文件大小：
  `size {{x86_64文件}} {{arm64文件}}`

- 显示文件的段大小并计算加载时间估算：
  `size -A {{目标文件}} | awk '/\.text/ {text=$2} /\.data/ {data=$2} END{print "Estimated load time:", (text+data)/1024/1024, "MB"}'`

- 显示文件的段大小并生成图表数据：
  `size -A {{目标文件}} | awk 'NR>1 && $2>0 {print $1, $2}' > {{图表数据文件}}`
