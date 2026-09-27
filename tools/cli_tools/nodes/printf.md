# printf

> 格式化并输出字符串和数字。
> 更多信息：<https://manned.org/printf>

- 输出普通字符串：
  `printf "{{字符串}}"`

- 输出字符串并换行：
  `printf "{{字符串}}\n"`

- 输出多个字符串：
  `printf "{{字符串1}} {{字符串2}} {{字符串3}}\n"`

- 使用格式化输出整数：
  `printf "%d\n" {{整数}}`

- 使用格式化输出浮点数：
  `printf "%f\n" {{浮点数}}`

- 使用格式化输出字符串：
  `printf "%s\n" "{{字符串}}"`

- 指定输出宽度：
  `printf "%10s\n" "{{字符串}}"`

- 左对齐输出：
  `printf "%-10s\n" "{{字符串}}"`

- 输出十六进制数：
  `printf "0x%x\n" {{整数}}`

- 输出八进制数：
  `printf "0%o\n" {{整数}}`

- 输出科学计数法：
  `printf "%e\n" {{浮点数}}`

- 控制小数位数：
  `printf "%.2f\n" {{浮点数}}`

- 输出多个格式化参数：
  `printf "%s %d %f\n" "{{字符串}}" {{整数}} {{浮点数}}`

- 使用转义字符：
  `printf "Tab:\tNewline:\nQuote:\"\n"`

- 输出变量值：
  `printf "Value: %s\n" "{{${变量}}}"`

- 格式化输出日期：
  `printf "Date: %(%Y-%m-%d)T\n" -1`

- 格式化输出时间：
  `printf "Time: %(%H:%M:%S)T\n" -1`

- 输出颜色文本：
  `printf "\033[31m%s\033[0m\n" "{{红色文本}}"`

- 输出带背景色的文本：
  `printf "\033[43;30m%s\033[0m\n" "{{黄色背景黑色文本}}"`

- 输出粗体文本：
  `printf "\033[1m%s\033[0m\n" "{{粗体文本}}"`

- 输出下划线文本：
  `printf "\033[4m%s\033[0m\n" "{{下划线文本}}"`

- 输出闪烁文本：
  `printf "\033[5m%s\033[0m\n" "{{闪烁文本}}"`

- 输出反色文本：
  `printf "\033[7m%s\033[0m\n" "{{反色文本}}"`

- 输出带边框的文本：
  `printf "+--------+\n| %s |\n+--------+\n" "{{文本}}"`

- 输出进度条：
  `printf "\r[%-20s] %d%%" "$(printf "%*s" ${{百分比}} | tr ' ' '=')" ${{百分比}}`

- 输出表格格式：
  `printf "%-10s %8s %6s\n" "Name" "Age" "Score"`

- 输出分隔线：
  `printf "%-30s\n" "$(printf '%*s' 30 | tr ' ' '-')"`

- 输出带前导零的数字：
  `printf "%04d\n" {{数字}}`

- 输出带千位分隔符的数字：
  `printf "%'d\n" {{数字}}`

- 输出百分比：
  `printf "%.2f%%\n" $(({{数值}} * 100.0 / {{总数}}))`

- 输出文件大小（KB）：
  `printf "%.2f KB\n" $(echo "{{字节数}}/1024" | bc -l)`

- 输出文件大小（MB）：
  `printf "%.2f MB\n" $(echo "{{字节数}}/1048576" | bc -l)`

- 输出文件大小（GB）：
  `printf "%.2f GB\n" $(echo "{{字节数}}/1073741824" | bc -l)`

- 输出二进制数：
  `printf "0b%08b\n" {{整数}}`

- 输出 IP 地址格式：
  `printf "%d.%d.%d.%d\n" ${{八位1}} ${{八位2}} ${{八位3}} ${{八位4}}`

- 输出 MAC 地址格式：
  `printf "%02x:%02x:%02x:%02x:%02x:%02x\n" ${{字节1}} ${{字节2}} ${{字节3}} ${{字节4}} ${{字节5}} ${{字节6}}`

- 输出十六进制转义序列：
  `printf "\x48\x65\x6c\x6c\x6f\n"`

- 输出八进制转义序列：
  `printf "\110\145\154\154\157\n"`

- 输出 Unicode 字符：
  `printf "\u0048\u0065\u006c\u006c\u006f\n"`

- 输出控制字符：
  `printf "\a\033[1G"` # 响铃并移动到行首

- 输出制表符对齐的列：
  `printf "%-20s\t%s\n" "{{列1}}" "{{列2}}"`

- 输出固定宽度的文本块：
  `printf "%-30s | %-30s | %-30s\n" "{{文本1}}" "{{文本2}}" "{{文本3}}"`

- 输出带符号的数字：
  `printf "%+d\n" {{数字}}`

- 输出空格填充：
  `printf "%*s\n" {{宽度}} "{{文本}}"`

- 输出动态宽度：
  `printf "%-*s\n" ${{宽度变量}} "{{文本}}"`

- 输出十六进制转储：
  `printf "%02x " "'{{字符}}"`

- 输出字符的 ASCII 值：
  `printf "%d\n" "'{{字符}}"`

- 输出数组元素：
  `printf "%s\n" "${{数组[@]}}"`

- 输出关联数组：
  `printf "%s: %s\n" "{{key}}" "${{array[key]}}"`

- 输出环境变量：
  `printf "%s=%s\n" "{{变量名}}" "${{变量名}}"`

- 输出函数调用结果：
  `printf "Result: %s\n" "$(function_name {{参数}})"`

- 输出命令执行结果：
  `printf "Output: %s\n" "$(command {{参数}})"`

- 输出条件判断结果：
  `printf "Status: %s\n" "$([[ {{条件}} ]] && echo "OK" || echo "FAIL")"`

- 输出数学计算结果：
  `printf "Calculation: %d\n" $(({{表达式}}))`

- 输出浮点数计算：
  `printf "Result: %.2f\n" $(echo "{{表达式}}" | bc -l)`

- 输出随机数：
  `printf "Random: %d\n" $((RANDOM % {{范围}} + {{最小值}}))`

- 输出当前时间戳：
  `printf "Timestamp: %s\n" $(date +%s)`

- 输出格式化的时间：
  `printf "Time: %(%Y-%m-%d %H:%M:%S)T\n" -1`

- 输出倒计时：
  `for i in {{5..1}}; do printf "\rCountdown: %d" $i; sleep 1; done; printf "\rDone!\n"`

- 输出进度指示器：
  `printf "Processing" && for i in {1..5}; do printf "."; sleep 1; done; printf " Complete\n"`

- 输出螺旋文本：
  `for i in {1..10}; do printf "%*s\n" $i "{{文本}}"; done`

- 输出金字塔：
  `for i in {1..5}; do printf "%*s\n" $i "$(printf "%*s" $((2*i-1)) | tr ' ' '*')"; done`

- 输出菱形：
  `for i in {1..5}; do printf "%*s\n" $i "$(printf "%*s" $((2*i-1)) | tr ' ' '*')"; done; for i in {4..1}; do printf "%*s\n" $i "$(printf "%*s" $((2*i-1)) | tr ' ' '*')"; done`

- 输出乘法表：
  `for i in {1..9}; do for j in {1..9}; do printf "%2d*%d=%-2d " $j $i $((i*j)); done; printf "\n"; done`

- 输出斐波那契数列：
  `a=0; b=1; for i in {1..10}; do printf "%d " $a; temp=$a; a=$b; b=$((temp+b)); done; printf "\n"`

- 输出质数：
  `for n in {2..50}; do is_prime=1; for i in $(seq 2 $((n/2))); do [ $((n%i)) -eq 0 ] && is_prime=0 && break; done; [ $is_prime -eq 1 ] && printf "%d " $n; done; printf "\n"`

- 输出数字的平方：
  `for i in {1..10}; do printf "%d squared is %d\n" $i $((i*i)); done`

- 输出数字的立方：
  `for i in {1..10}; do printf "%d cubed is %d\n" $i $((i*i*i)); done`

- 输出数字的阶乘：
  `for i in {1..10}; do fact=1; for j in $(seq 1 $i); do fact=$((fact*j)); done; printf "%d! = %d\n" $i $fact; done`
