# nice

> 以修改后的调度优先级运行命令。
> 更多信息：<https://manned.org/nice>

- 使用默认优先级（增加 10）运行命令：
  `nice {{命令}}`

- 指定优先级值运行命令（-20 最高，19 最低）：
  `nice -n {{优先级}} {{命令}}`

- 以高优先级运行命令（需要 root 权限）：
  `sudo nice -n -10 {{命令}}`

- 以低优先级运行命令：
  `nice -n 15 {{命令}}`

- 查看当前 nice 值：
  `nice`

- 运行 CPU 密集型任务（降低优先级）：
  `nice -n 19 make`

- 运行重要系统进程（提高优先级）：
  `sudo nice -n -5 systemctl restart {{服务名}}`

- 组合使用 nice 和其他命令：
  `nice -n 10 ionice -c2 -n7 {{命令}}`

- 在后台运行低优先级任务：
  `nice -n 15 {{命令}} &`

- 查看进程的 nice 值：
  `ps -eo pid,ni,comm | grep {{进程名}}`

- 批量处理文件时降低优先级：
  `nice -n 10 find {{目录}} -name "{{模式}}" -exec {{命令}} {} \;`

- 编译大型项目时降低优先级：
  `nice -n 15 make -j{{核心数}}`

- 压缩大文件时降低优先级：
  `nice -n 19 tar -czf {{压缩包}} {{目录}}`

- 运行数据库备份（中等优先级）：
  `nice -n 5 mysqldump -u {{用户}} -p{{密码}} {{数据库}} > {{备份文件}}`

- 运行网络下载任务（低优先级）：
  `nice -n 15 wget {{URL}}`

- 运行系统监控脚本（高优先级）：
  `sudo nice -n -10 {{监控脚本}}`

- 测试程序性能时设置特定优先级：
  `nice -n 0 {{测试程序}}`

- 运行多进程任务时平衡负载：
  `nice -n 10 parallel {{命令}} ::: {{参数列表}}`

- 在服务器上运行非关键任务：
  `nice -n 15 {{脚本}} > {{日志文件}} 2>&1 &`

- 运行科学计算任务（低优先级）：
  `nice -n 19 python {{计算脚本}}.py`

- 查看系统默认 nice 值：
  `cat /proc/sys/kernel/nice`

- 修改系统默认 nice 范围（需要 root）：
  `sudo sysctl kernel.nice={{值}}`