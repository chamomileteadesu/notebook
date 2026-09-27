# AWK

- [AWK](#awk)
  - [CLI 基本用法](#cli-基本用法)
  - [AWK 程式碼結構](#awk-程式碼結構)
  - [內建變數](#內建變數)
  - [內建函數](#內建函數)
    - [數學函數](#數學函數)
    - [字串函數](#字串函數)
  - [基礎範例](#基礎範例)
  - [進階語法與技巧](#進階語法與技巧)
    - [自訂欄位分隔符](#自訂欄位分隔符)
    - [條件判斷](#條件判斷)
    - [函數](#函數)
    - [正規表示式](#正規表示式)
    - [陣列](#陣列)

## CLI 基本用法

```shell
awk '程式碼' 檔案
# or
awk -f script.awk 檔案
# 傳入外部變數
awk -v threshold=100 '$3 > threshold' file.txt
# 多檔案處理
awk '{print FILENAME, NR, $0}' file1.txt file2.txt
```

## AWK 程式碼結構

```awk
BEGIN { 
    # 程式開始前執行一次
}

PATTERN { 
    ACTTION 
}

END { 
    # 所有處理結束後執行一次
}
```

awk 的基本格式永遠是：

`awk 'pattern { action }' 文件名`

- pattern：決定「這一行要不要處理」。
- action：決定「如果要處理，要做什麼」。
- 整個腳本用單引號包起來，避免 shell 誤解。
- 可以有多組 pattern { action }，awk 會一行一行掃描輸入。
- pattern 可以省略 → 表示「每一行都處理」。
- action 可以省略 → 預設動作是 print（印出整行）。
- 但不能兩個都省略
- 特殊 pattern：
  - BEGIN { ... } → 在處理任何一行之前執行一次（常用來印標題、設變數）。
  - END { ... } → 在處理完所有行之後執行一次（常用來印總計）。

## 內建變數

| 變數 | 意義 |
| - | - |
| `$0` | 目前整行內容 |
| `$1 $2...` | 第 1、2... 個欄位 |
| `NF` | 目前這一行有多少個欄位 |
| `NR` | 目前處理到第幾行（行號） |
| `FNR` | 目前檔案的行號（多檔時重置） |
| `FS` | 欄位分隔符（預設空白） |
| `OFS` | 輸出欄位分隔符（預設空白） |
| `RS` | 記錄分隔符（預設換行） |
| `ORS` | 輸出記錄分隔符 |
| `FILENAME` | 目前處理的檔案名稱 |

## 內建函數

### 數學函數

- int()
- sqrt()
- log()
- exp()
- rand()

### 字串函數

- printf("%s", $1): 格式化打印字串
- length($0)：字串長度
- substr($0, 開始位置, 長度)
- index(字串, 子字串)
- match(字串, 正規表示式)
- gsub(/正規/, "替換", 字串)：全域替換
- tolower()
- toupper()

## 基礎範例

範例 1：印出第 1 欄和第 3 欄

```shell
awk '{print $1, $3}' access.log
```

範例 2：只處理特定模式

```shell
# 印出含有 "ERROR" 的行
awk '/ERROR/' error.log

# 印出第 1 欄是 "root" 的行
awk '$1 == "root"' /etc/passwd
```

範例 3：計算欄位總和

```shell
# 計算 access.log 中第 10 欄（通常是 bytes）總和
awk '{sum += $10} END {print sum}' access.log
```

範例 4：計算平均值

```shell
awk '{sum += $10; n++} END {print sum/n}' access.log
```

範例 5：輸出到文件

```shell
awk '/ERROR/ {print $0 >> "error.log"}' access.log
```

## 進階語法與技巧

### 自訂欄位分隔符

```shell
# 以逗號為分隔符處理 CSV
awk -F, '{print $1, $2}' data.csv

# 以冒號為分隔符處理 /etc/passwd
awk -F: '{print $1, $7}' /etc/passwd
```

### 條件判斷

```shell
# 第 3 欄大於 100 的行
awk '$3 > 100 {print $0}' file.txt

# 多條件
awk '$1 == "user" && $3 > 5000' file.log
```

### 函數

```shell
# 印出第 1 欄長度大於 10 的行
awk 'length($1) > 10' file.txt

# 不含 "foo" 的行（! 是反向）
awk '!/foo/' file.txt

# 把所有大寫轉小寫
awk '{print tolower($0)}' file.txt
```

### 正規表示式

```shell
# 以數字開頭的行
awk '/^[0-9]/' file.txt

# 第 1 欄是 email 格式
awk '$1 ~ /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/' emails.txt
```

### 陣列

```shell
# 統計每個 IP 出現次數
awk '{ip[$1]++} END {for(i in ip) print i, ip[i]}' access.log

# 統計 HTTP 狀態碼次數
awk '{status[$9]++} END {for(s in status) print s, status[s]}' access.log
```
