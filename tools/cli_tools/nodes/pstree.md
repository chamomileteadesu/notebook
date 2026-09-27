# pstree

> 以树状图显示进程，展示进程间的父子关系。
> 更多信息：<https://manned.org/pstree>

- 显示完整的进程树：
  `pstree`

- 显示指定 PID 的进程树：
  `pstree {{进程ID}}`

- 显示指定用户的进程树：
  `pstree {{用户名}}`

- 显示进程 PID：
  `pstree -p`

- 显示完整命令行参数：
  `pstree -a`

- 高亮显示当前进程：
  `pstree -h`

- 显示进程的用户和组 ID：
  `pstree -u`

- 按进程 ID 排序：
  `pstree -n`

- 压缩相同的子进程：
  `pstree -c`

- 显示进程间的线程：
  `pstree -T`

- 不换行显示进程树：
  `pstree -l`

- 显示 ASCII 字符而非线条：
  `pstree -A`

- 显示指定进程的详细树：
  `pstree -p -a {{进程名}}`

- 查看系统初始化进程树：
  `pstree -p 1`

- 显示所有用户的进程树并包含 PID：
  `pstree -a -u -p`

- 查看特定进程的所有子进程：
  `pstree -p -a $(pgrep {{进程名}} | head -1)`

- 显示进程树并统计进程数量：
  `pstree -p | wc -l`

- 查看容器内的进程树：
  `pstree -p -a | grep {{容器进程}}`

- 监控进程树变化：
  `watch "pstree -p -a"`

- 显示进程树并保存到文件：
  `pstree -p -a > {{进程树文件}}`

- 查看指定终端的进程树：
  `pstree -p -a -t {{终端设备}}`

- 显示进程树并过滤特定进程：
  `pstree -p -a | grep {{进程名}}`

- 查看进程的资源使用情况树状视图：
  `pstree -p -a | xargs -I {} ps -p {} -o pid,ppid,cmd,%cpu,%mem --no-headers`

- 显示进程树并查找僵尸进程：
  `pstree -p -a | grep "<defunct>"`

- 查看进程的完整继承关系：
  `pstree -p -a -H {{进程ID}}`

- 显示进程树并按 CPU 使用率排序：
  `for pid in $(pstree -p | grep -o '\([0-9]\+\)' | tr -d '()'); do
    ps -p $pid -o pid,pcpu,cmd --no-headers
  done | sort -k2 -nr`

- 查看特定用户的进程树：
  `pstree -p -a -u {{用户名}}`

- 显示进程树并高亮显示特定进程：
  `pstree -p -a | grep --color=auto {{进程名}}`

- 查看系统服务的进程树：
  `pstree -p -a | grep systemd`

- 监控进程树的实时变化：
  `while true; do
    clear
    pstree -p -a
    sleep 2
  done`

- 显示进程树并统计每个进程的子进程数：
  `pstree -p | awk -F'[---]' '{print $1, NF-1}'`

- 查看进程树并查找内存使用最高的进程：
  `pstree -p | xargs -I {} ps -p {} -o pid,rss,cmd --no-headers | sort -k2 -nr`

- 显示进程树并按启动时间排序：
  `pstree -p | xargs -I {} ps -p {} -o pid,lstart,cmd --no-headers | sort -k2`