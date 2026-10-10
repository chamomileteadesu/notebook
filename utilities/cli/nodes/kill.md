# kill

> 向进程发送信号（通常用于终止进程）。
> 更多信息：<https://manned.org/kill>

- 终止进程（默认发送 SIGTERM）：
  `kill {{PID}}`

- 强制终止进程（SIGKILL）：
  `kill -9 {{PID}}`

- 挂起进程（SIGSTOP）：
  `kill -STOP {{PID}}`

- 继续运行挂起的进程（SIGCONT）：
  `kill -CONT {{PID}}`

- 友好地请求进程终止（SIGTERM，默认信号）：
  `kill -TERM {{PID}}`

- 中断进程（SIGINT，等同于 Ctrl+C）：
  `kill -INT {{PID}}`

- 列出所有可用信号：
  `kill -l`

- 向指定进程组发送信号：
  `kill -{{信号}} -{{PGID}}`
