# disown

> 从 shell 的活动作业表中移除作业，使其不受 shell 终端的影响。
> 更多信息：<https://manned.org/disown>

- 移除当前作业：
  `disown`

- 移除指定作业号：
  `disown %{{作业号}}`

- 移除指定进程 ID：
  `disown -h {{进程ID}}`

- 移除所有作业：
  `disown -a`

- 移除所有正在运行的作业：
  `disown -r`

- 移除作业并防止其被挂起：
  `disown -h %{{作业号}}`

- 启动命令后立即移除：
  `{{命令}} & disown`

- 启动命令并移除所有输出：
  `{{命令}} > /dev/null 2>&1 & disown`

- 查看当前作业列表：
  `jobs`

- 移除作业并确认：
  `disown %{{作业号}} && echo "作业已移除"`

- 移除多个作业：
  `disown %{{作业号1}} %{{作业号2}}`

- 移除作业并记录 PID：
  `disown -p %{{作业号}}`

- 启动长时间运行任务并移除：
  `nohup {{长时间任务}} > {{日志文件}} 2>&1 & disown`

- 移除作业但不终止：
  `disown -h %{{作业号}}`

- 移除所有后台作业：
  `disown -a && echo "所有后台作业已移除"`

- 启动服务并移除：
  `{{服务启动命令}} > {{服务日志}} 2>&1 & disown -h`

- 移除作业并保存 PID 到文件：
  `disown -p %{{作业号}} > {{PID文件}}`

- 批量移除匹配的作业：
  `jobs | grep {{模式}} | awk '{print $1}' | xargs -I {} disown {}`

- 移除作业并设置环境变量：
  `VAR={{值}} {{命令}} & disown`

- 移除作业并发送信号：
  `disown %{{作业号}} && kill -USR1 %{{作业号}}`

- 安全移除作业（检查是否存在）：
  `jobs | grep -q "%{{作业号}}" && disown %{{作业号}}`

- 移除作业并记录到系统日志：
  `disown %{{作业号}} && logger "作业 %{{作业号}} 已移除"`

- 启动监控脚本并移除：
  `{{监控脚本}} > {{监控日志}} 2>&1 & disown -h`

- 移除作业并清理临时文件：
  `disown %{{作业号}} && rm -f {{临时文件}}`

- 移除所有作业并显示统计：
  `disown -a && echo "已移除 $(jobs -p | wc -l) 个作业"`

- 移除作业并更新状态文件：
  `disown %{{作业号}} && echo "$(date): 作业移除" >> {{状态文件}}`

- 启动批处理任务并移除：
  `for task in {{任务列表}}; do
    $task > ${task}.log 2>&1 & disown
  done`

- 移除作业并发送通知：
  `disown %{{作业号}} && notify-send "作业已移除" "作业 %{{作业号}} 已从 shell 移除"`
