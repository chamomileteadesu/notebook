# Sed 語法

## sed 的基本執行流程

- 讀取輸入流的一行到模式空間。
- 檢查該行是否符合「地址」（address），若符合則執行對應的「命令」（command）。
- 處理完後，預設自動將模式空間內容輸出到標準輸出。
- 清空模式空間，繼續處理下一行。

## 命令列基本語法

```shell
sed [選項] '地址 命令' 檔案
# 或從管道讀取
命令 | sed [選項] '地址 命令'
```

常用選項：

- -n（或 --quiet）：安靜模式，取消自動輸出（需搭配 p 命令才會輸出）。
- -i（或 -i.bak）：就地編輯，直接修改原檔案（建議加 .bak 備份）。
- -r 或 -E：使用擴展正則表達式（推薦，+ ? () {} 等不用轉義）。
- -e：執行多個腳本命令。
- -f scriptfile：從腳本檔案讀取命令。

## 地址

地址決定命令作用的範圍，寫在命令前面，可省略（表示處理所有行）。

地址形式：

- 行號：5（第 5 行）、1,10（第 1 到 10 行）、$（最後一行）。
- 正則匹配：/pattern/（包含 pattern 的行），如 /error/。
- 範圍組合：1,/pattern/（從第 1 行到第一個匹配 pattern 的行）。
- 取反：!（例如 5!d 表示「除了第 5 行外都刪除」）。
- 多地址：用逗號分隔，或用 { } 群組多個命令。

範例：

```shell
# 只打印第 5 行（需搭配 -n 才不會重複輸出）
sed '5p' file.txt
# 刪除以 # 開頭的註解行
sed '/^#/d' config.txt
# 只在第 1-10 行進行替換
sed '1,10s/old/new/g' 
# 打印從開頭到第一個 ERROR 的內容
sed -n '1,/ERROR/p' log
```

## 常用命令

sed 命令通常是單字母，寫在地址後面。

### 替換命令 s（substitute）

語法：`s/搜尋模式/替換內容/標誌`

標誌（flags）：

- g：全局替換（一行內所有匹配都替換）。
- 數字（如 2）：只替換第幾次出現。
- p：打印替換後的行（常與 -n 搭配）。
- i 或 I：忽略大小寫（GNU sed）。
- &：代表整個匹配到的內容。
- \1, \2 ...：反向引用分組內容（需用 \( \) 或擴展正則 ()）。

範例：

```shell
# 基本替換
sed 's/hello/Hi/' file.txt

# 全局替換 + 忽略大小寫
sed 's/linux/Linux/gi' file.txt

# 使用不同分隔符（當內容含 / 時很方便）
sed 's@/usr/local@/opt@g' paths.txt

# 使用 & 和分組
sed 's/\(Linux\)/\1 is great/' file.txt     # → Linux is great
sed -r 's/(Linux)/\1 rocks/' file.txt       # 使用 -r 不用轉義

# 只替換第 2 行，並打印修改過的行
sed -n '2s/old/new/p' file.txt
```

### 刪除命令 d（delete）

```shell
sed '2d' file.txt           # 刪除第 2 行
sed '/^$/d' file.txt        # 刪除空行
sed '1,10d' file.txt        # 刪除前 10 行
sed '/pattern/!d' file.txt  # 只保留匹配 pattern 的行（取反用法）
```

### 打印命令 p（print）

通常與 -n 搭配，只輸出符合條件的行：

```shell
sed -n '/error/p' log.txt
sed -n '5,10p' file.txt
```

### 插入、追加、替換整行

- i\：在當前行前面插入。
- a\：在當前行後面追加。
- c\：替換整行為新內容。

```shell
sed '2i\這是插入的新行' file.txt
sed '/pattern/a\這是追加的內容' file.txt
sed '3c\整行被替換為這句話' file.txt
```

### 其他常用命令

- =：打印行號。
- y/abc/def/：字符逐一轉換（a→d、b→e、c→f）。
- q：退出 sed（處理到某行後停止）。
- r file：讀取另一個檔案內容插入。
- w file：將模式空間寫入檔案。

## 多命令與腳本寫法

在一行內執行多個命令：

- 使用分號 ; 分隔：sed 's/old/new/g; /error/d' file
- 使用 -e：sed -e 's/old/new/g' -e '/error/d' file

使用大括號 { } 對同一地址執行多命令：

```shell
sed '/pattern/{
  s/old/new/g
  p
  d
}' file.txt
```

從腳本檔案執行：

```shell
cat > mysed.sed <<EOF
s/old/new/g
/error/d
EOF
sed -f mysed.sed file.txt
```
