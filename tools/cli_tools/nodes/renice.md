# renice

> 修改正在运行进程的调度优先级。
> 更多信息：<https://manned.org/renice>

- 修改指定进程的优先级：
  `renice {{优先级}} {{进程ID}}`

- 修改多个进程的优先级：
  `renice {{优先级}} {{进程ID1}} {{进程ID2}} {{进程ID3}}`

- 修改用户所有进程的优先级：
  `renice {{优先级}} -u {{用户名}}`

- 修改组所有进程的优先级：
  `renice {{优先级}} -g {{组名}}`

- 修改指定进程组所有进程的优先级：
  `renice {{优先级}} -p {{进程组ID}}`

- 降低进程优先级（使其更"友好"）：
  `renice 10 {{进程ID}}`

- 提高进程优先级（需要 root 权限）：
  `sudo renice -5 {{进程ID}}`

- 设置最低优先级（几乎不占用 CPU）：
  `renice 19 {{进程ID}}`

- 设置最高优先级（需要 root）：
  `sudo renice -20 {{进程ID}}`

- 修改后台任务的优先级：
  `renice 15 %1`

- 批量修改相似进程的优先级：
  `pgrep {{进程名}} | xargs renice {{优先级}}`

- 降低所有用户进程的优先级：
  `renice 10 -u {{用户名}}`

- 提高系统关键进程的优先级：
  `sudo renice -5 $(pgrep {{关键进程名}})`

- 降低编译进程的优先级：
  `ps aux | grep make | awk '{print $2}' | xargs renice 15`

- 降低下载进程的优先级：
  `renice 15 $(pgrep -f wget)`

- 提高数据库进程的优先级：
  `sudo renice -5 $(pgrep mysqld)`

- 查看修改后的优先级：
  `ps -eo pid,ni,comm | grep {{进程ID}}`

- 修改所有非根进程的优先级：
  `sudo renice 5 -u $(awk -F: '$3>999 {print $1}' /etc/passwd | tr '\n' ',' | sed 's/,$//')`

- 降低科学计算进程的优先级：
  `renice 19 $(pgrep -f python.*计算)`

- 提高系统监控进程的优先级：
  `sudo renice -10 $(pgrep -f {{监控服务}})`

- 修改容器进程的优先级：
  `renice 10 $(pgrep -f docker)`

- 降低备份进程的优先级：
  `renice 15 $(pgrep rsync)`

- 动态调整进程优先级脚本：
  ```bash
  #!/bin/bash
  while true; do
    # 如果 CPU 使用率超过 80%，降低优先级
    ps aux --sort=-%cpu | head -10 | awk '$3 > 80 && $1 != "root" {print $2}' | xargs renice 10
    sleep 60
  done
  ```

- 安全地降低进程优先级（检查进程是否存在）：
  `kill -0 {{进程ID}} 2>/dev/null && renice {{优先级}} {{进程ID}}`

- 查看当前系统的优先级分布：
  `ps -eo ni= | sort -n | uniq -c`

- 恢复进程到默认优先级：
  `renice 0 {{进程ID}}`