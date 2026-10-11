# Automatic Repeat Request(ARQ)

> ARQ 本身是解决可靠传输的，但是提到的滑动窗口机制也常用于流量控制。

> [!note]
> ARQ 只是算法思想，不限于网络层次，TCP/IP 通常在鏈路層和傳輸層使用 ARQ 解决各层的问题。
> 例如：以太网由于其环境相对稳定，在鏈路層没有 ARQ 机制；而由于无线环境相对复杂，802.11 在鏈路層就需要 ARQ。为了方便描述，以下将 PDU 统称为「帧」。

常用的 ARQ 算法：

- [[stop_wait]]
- [[go_back_n]]
- [[selective_repeat]]
