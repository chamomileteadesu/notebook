# Bash 語法

- [Bash 語法](#bash-語法)
  - [變數與資料型態](#變數與資料型態)
  - [條件判斷](#條件判斷)
    - [if 語句](#if-語句)
    - [case 語句](#case-語句)
  - [迴圈](#迴圈)
    - [for 迴圈](#for-迴圈)
    - [while 迴圈](#while-迴圈)
  - [函數](#函數)
  - [錯誤處理與除錯](#錯誤處理與除錯)

## 變數與資料型態

變數類型：

- 字串（預設）
- 整數
- 陣列

```shell
# 定義變數（注意：等號兩邊不能有空格）
name="foo"
age=28
is_student=true

# 使用變數
echo "我的名字是 ${name}，今年 ${age} 歲"

# 陣列
fruits=("蘋果" "香蕉" "橘子")
# 蘋果
echo ${fruits[0]}
# 所有元素
echo ${fruits[@]}
# 元素個數
echo ${#fruits[@]}

# 特殊變數
echo "腳本檔名：$0"
echo "第一個參數：$1"
echo "所有參數：$@"
echo "所有參數：$*"
echo "參數個數：$#"
echo "目前行程 ID：$$"
echo "上一個指令的返回值：$?"
```

## 條件判斷

### if 語句

```shell
score=85

if [ $score -ge 90 ]; then
    echo "優秀"
elif [ $score -ge 80 ]; then
    echo "良好"
elif [ $score -ge 60 ]; then
    echo "及格"
else
    echo "不及格"
fi
```

常用條件測試：

- -eq、 -ne、 -gt、 -ge、 -lt、 -le（數值比較）
- =、 !=（字串比較）
- -f（是否為普通檔案）
- -d（是否為目錄）
- -r、 -w、 -x（權限判斷）
- -z（字串是否為空）

### case 語句

```shell
read -p "輸入一個數字 (1-3)：" num

case $num in
    1) echo "你輸入的是 1" ;;
    2) echo "你輸入的是 2" ;;
    3) echo "你輸入的是 3" ;;
    *) echo "輸入無效！" ;;
esac
```

## 迴圈

### for 迴圈

```shell
# 傳統 for
for i in {1..5}; do
    echo "第 $i 次循環"
done

# 迭代陣列或檔案
for file in *.txt; do
    echo "處理檔案：$file"
done

# C 語言風格
for ((i=0; i<10; i++)); do
    echo $i
done
```

### while 迴圈

```shell
count=1
while [ $count -le 5 ]; do
    echo "計數：$count"
    ((count++))
done
```

## 函數

```shell
# 定義函數
greet() {
    local name=$1          # local 變數只在函數內有效
    echo "你好，${name}！"
    return 0               # 返回值（慣例 0 代表成功）
}

# 呼叫函數
greet "Chamomile"

# 帶多個參數
add() {
    echo $(( $1 + $2 ))
}

result=$(add 3 7)
echo "3 + 7 = ${result}"
```

## 錯誤處理與除錯

```shell
set -e          # 任何指令失敗就立即退出腳本
set -u          # 使用未定義變數時視為錯誤
set -x          # 除錯模式，顯示每一步執行指令
set -o pipefail # 管線中任何指令失敗都視為失敗

# 捕捉錯誤
trap 'echo "發生錯誤！行號：$LINENO"' ERR
```
