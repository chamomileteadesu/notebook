# tr

> 转换或删除字符（只能从标准输入读取）。
> 更多信息：<https://manned.org/tr>

- 将小写转换为大写：
  `echo "{{hello}}" | tr 'a-z' 'A-Z'`

- 删除指定字符：
  `echo "{{hello123}}" | tr -d '0-9'`

- 压缩重复字符：
  `echo "{{hello    world}}" | tr -s ' '`

- 替换字符：
  `echo "{{hello}}" | tr 'a-z' 'A-Z'`

- 删除所有非数字字符：
  `echo "{{hello123}}" | tr -cd '0-9'`

- 将换行符替换为空格：
  `cat {{文件}} | tr '\n' ' '`

- 删除控制字符：
  `cat {{文件}} | tr -d '\r'`
