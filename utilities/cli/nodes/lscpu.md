# lscpu

> 显示 CPU 架构信息。
> 更多信息：<https://manned.org/lscpu>

- 显示 CPU 的基本信息：
  `lscpu`

- 以可解析格式显示 CPU 信息：
  `lscpu -e`

- 显示扩展的 CPU 信息：
  `lscpu -e --extended`

- 显示物理 CPU 数量：
  `lscpu | grep "CPU(s):"`

- 显示核心数量：
  `lscpu | grep "Core(s)"`

- 显示线程数量：
  `lscpu | grep "Thread(s)"`

- 显示 CPU 架构：
  `lscpu | grep "Architecture"`

- 显示 CPU 运行模式：
  `lscpu | grep "CPU op-mode(s)"`

- 显示字节序：
  `lscpu | grep "Byte Order"`

- 显示 CPU 型号：
  `lscpu | grep "Model name"`

- 显示 CPU 家族：
  `lscpu | grep "CPU family"`

- 显示步进：
  `lscpu | grep "Stepping"`

- 显示 CPU 主频：
  `lscpu | grep "CPU MHz"`

- 显示最大主频：
  `lscpu | grep "CPU max MHz"`

- 显示最小主频：
  `lscpu | grep "CPU min MHz"`

- 显示缓存大小：
  `lscpu | grep "Cache"`

- 显示 L1 缓存信息：
  `lscpu | grep "L1d"`

- 显示 L2 缓存信息：
  `lscpu | grep "L2"`

- 显示 L3 缓存信息：
  `lscpu | grep "L3"`

- 显示 NUMA 节点信息：
  `lscpu | grep "NUMA node(s)"`

- 显示虚拟化支持：
  `lscpu | grep "Virtualization"`

- 显示超线程状态：
  `lscpu | grep "Hyper-threading"`

- 显示 CPU 特性标志：
  `lscpu | grep "Flags"`

- 显示特定 CPU 核心的信息：
  `lscpu -p {{核心号}}`

- 显示 CPU 拓扑信息：
  `lscpu --parse=CPU,Core,Socket`

- 显示 CPU 的物理 ID：
  `lscpu | grep "Physical ID"`

- 显示套接字数量：
  `lscpu | grep "Socket(s)"`

- 显示 NUMA 节点的 CPU 分布：
  `lscpu --parse=NUMA_NODE`

- 显示 CPU 的在线状态：
  `lscpu --online`

- 显示 CPU 的离线状态：
  `lscpu --offline`

- 显示所有 CPU 的详细信息：
  `lscpu -e --all`

- 显示 CPU 的缓存层次结构：
  `lscpu --cache`

- 显示 CPU 的虚拟化特性：
  `lscpu | grep -i "virt"`

- 显示 CPU 的安全特性：
  `lscpu | grep -i "security"`

- 显示 CPU 的大小端信息：
  `lscpu | grep -i "endian"`

- 显示 CPU 的型号名称：
  `lscpu | grep "Model name" | cut -d: -f2 | sed 's/^[ \t]*//'`

- 计算 CPU 的核心总数：
  `lscpu | grep "Core(s) per socket" | awk '{print $4}' * $(lscpu | grep "Socket(s)" | awk '{print $2}')`

- 显示 CPU 的缓存总大小：
  `lscpu | grep -E "L1|L2|L3" | awk '{sum+=$3} END{print "Total Cache:", sum/1024, "MB"}'`

- 检查是否支持 64 位：
  `lscpu | grep "CPU op-mode(s)" | grep -q "64-bit" && echo "64-bit supported" || echo "64-bit not supported"`

- 检查是否支持虚拟化：
  `lscpu | grep -i "virtualization" | grep -q "full" && echo "Full virtualization supported" || echo "Full virtualization not supported"`

- 显示 CPU 的频率范围：
  `lscpu | grep -E "(CPU max MHz|CPU min MHz|CPU MHz)"`

- 显示 CPU 的物理特性：
  `lscpu | grep -E "(BogoMIPS|Hypervisor)"`

- 显示 CPU 的 NUMA 拓扑：
  `lscpu --parse=NUMA_NODE,CPU`

- 显示 CPU 的功耗管理特性：
  `lscpu | grep -i "power"`

- 检查是否支持 AES 指令：
  `lscpu | grep "Flags" | grep -q "aes" && echo "AES supported" || echo "AES not supported"`

- 显示 CPU 的制造商信息：
  `lscpu | grep "Model name" | cut -d: -f2 | cut -d' ' -f1`

- 显示 CPU 的缓存行大小：
  `lscpu | grep "Cache" | grep "line" || cat /sys/devices/system/cpu/cpu0/cache/index0/coherency_line_size`

- 检查是否支持 AVX 指令：
  `lscpu | grep "Flags" | grep -q "avx" && echo "AVX supported" || echo "AVX not supported"`

- 显示 CPU 的温度信息（如果可用）：
  `lscpu && find /sys/devices/platform/ -name "temp*_input" -exec cat {} \;`

- 显示 CPU 的电源管理策略：
  `lscpu && cat /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor`

- 显示 CPU 的中断统计：
  `lscpu && cat /proc/interrupts | grep CPU`

- 监控 CPU 频率变化：
  `watch -n 1 "cat /proc/cpuinfo | grep MHz"`

- 显示 CPU 的负载均衡信息：
  `lscpu && cat /proc/softirqs | grep CPU`
