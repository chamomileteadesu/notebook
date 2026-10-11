# Medium Access Control

> 解决多个节点如何共享同一传输介质的问题，广播信道需要实现，点对点信道通常无需实现。

媒體訪問控制方案：

- 信道劃分
  - 采用[[channel_multiplexing|信道復用技術]]劃分信道
  - 采用接入技術
    - 时分多址 TDMA
    - 频分多址 FDMA
    - 码分多址 CDMA
- 隨機訪問
  - [[aloha_protocol|ALOHA 協議]]
  - [[csma_protocol|CSMA 協議]]
- 輪詢訪問
  - 例如[[token_passing|令牌傳遞協議]]
