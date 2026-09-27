# JQ Filter DSL

- [JQ Filter DSL](#jq-filter-dsl)
  - [Filter 基礎概念](#filter-基礎概念)
  - [物件欄位取值](#物件欄位取值)
  - [陣列處理](#陣列處理)
  - [管道](#管道)
  - [條件過濾](#條件過濾)
  - [重建新 JSON 物件](#重建新-json-物件)

## Filter 基礎概念

Filter 是放在單引號中的表達式，用來告訴 jq：「我要對 JSON 做什麼」。

基本規則：

- Filter 必須用單引號 `'...'` 包起來（避免被 shell 解析）
- 使用 `.` 來表示「當前資料」
- 語法類似「走路」：從根開始，一步一步走到你要的位置

## 物件欄位取值

假設 JSON 為 data.json:

```json
{
  "name": "小明",
  "age": 25,
  "isActive": true,
  "address": {
    "city": "台北",
    "district": "信義區"
  }
}
```

```shell
# 取出頂層欄位
jq '.name' data.json
jq '.age' data.json

# 取出巢狀欄位（用 . 連接）
jq '.address.city' data.json
jq '.address.district' data.json
```

## 陣列處理

語法：

- .陣列名稱[索引] → 取特定元素（索引從 0 開始）
- .陣列名稱[] → 展開陣列，每一個元素單獨輸出

範例 JSON:

```json
{
  "skills": ["Python", "JavaScript", "SQL", "Docker"],
  "projects": [
    {"id": 101, "title": "網站改版", "status": "done"},
    {"id": 102, "title": "App 開發", "status": "doing"},
    {"id": 103, "title": "資料分析", "status": "todo"}
  ]
}
```

```shell
# 取出第一個技能
jq '.skills[0]'
# 第二個技能
jq '.skills[1]'
# 最後一個技能
jq '.skills[-1]'

# 展開所有技能，每行一個
jq '.skills[]'
# 取出所有專案的標題
jq '.projects[].title'
```

## 管道

語法：

`左邊的Filter | 右邊的Filter`

範例：

```shell
# 先展開 projects，再取出每個專案的 title
jq '.projects[] | .title' data.json

# 先展開 skills，再加上前綴文字（需用 -r）
jq -r '.skills[] | "我會的技能：\(. )"' data.json
```

## 條件過濾

當你只想要符合某些條件的資料時，使用 `select()`。

常用條件：

- `=` 等於
- `!=` 不等於
- `>、<、>=、<=`
- `and、or`

範例：

```shell
# 取出 status 為 "doing" 的專案
jq '.projects[] | select(.status == "doing")' data.json

# 取出 age 大於等於 20 的人
jq 'select(.age >= 20)' data.json

# 多條件組合
jq '.projects[] | select(.status == "done" or .status == "doing")' data.json
```

## 重建新 JSON 物件

這是 jq 最實用的進階功能：把資料重新組合成你想要的格式。

語法：

`{ 新欄位名: 值, 新欄位名: 值 }`

範例：

```shell
# 只保留 name 和 city，組成新物件
jq '{name: .name, city: .address.city}' data.json

# 對陣列中的每個元素重建物件
jq '.projects[] | {
    project_id: .id,
    project_name: .title,
    completed: (.status == "done")
}' data.json

# 簡寫：欄位名相同時可直接寫欄位名
jq '.projects[] | {id, title, status}' data.json
```
