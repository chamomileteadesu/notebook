# Hash Table

- Basic Concepts
  - Hash Table Definition: 一种通过关键字计算資料元素存储地址的資料結構
  - Hash Collision：兩個或更多不同的鍵（Key）經過哈希函數計算後，得到了相同的哈希值
  - Synonym：具有相同哈希值的不同鍵
  - Load Factor： 哈希表中已存儲的元素個數與哈希表總桶數（或總槽位數）的比值
- 哈希函數
  - [[direct-addressing|直接定址法]]
  - [[division-method|除留余数法]]
  - [[digit-analysis-method|数字分析法]]
  - [[mid-square-method|平方取中法]]
- 碰撞處理
  - [[separate_chaining|拉鏈法]]
  - [[open_addressing|開放地址法]]
