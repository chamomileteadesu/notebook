# Carrier Sense Multiple Access(CSMA) Protocol

> CSMA 是数据链路层通信中常用的一種“**先听后说**”协议族，不同坚持算法（1-坚持、非坚持、p-坚持）描述当线路忙碌时要等待多久，CD/CA 變體则描述了在开始传输后如何处理冲突（通常還定義了侦听行为）。

基於不同堅持算法的 CSMA 變體：

- [[1-persistent_csma|1-persistent CSMA]]
- [[non-persistent_csma|Non-persistent CSMA]]
- [[p-persistent_csma|p-persistent CSMA]]

基於不同衝突處理方法的 CSMA 變體：

- [[csma_collision-detection|CSMA/CD]](Collision Detection, Usually 1-persistent)
- [[csma_collision-avoidance|CSMA/CA]](Collision Avoidance, Usually p-persistent)
