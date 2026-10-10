# lsmod

> 显示已加载的内核模块。
> 更多信息：<https://manned.org/lsmod>

- 显示所有已加载的内核模块：
  `lsmod`

- 显示模块的大小信息：
  `lsmod | awk '{print $1, $2}'`

- 查找特定模块：
  `lsmod | grep {{模块名}}`

- 按模块大小排序：
  `lsmod | sort -k2 -nr`

- 显示被使用次数最多的模块：
  `lsmod | sort -k3 -nr | head -10`

- 显示最大的模块：
  `lsmod | awk 'NR>1 {print $1, $2}' | sort -k2 -nr | head -10`

- 统计已加载模块的数量：
  `lsmod | wc -l`

- 查找网络相关的模块：
  `lsmod | grep -i "net\|eth\|wifi\|bluetooth"`

- 查找文件系统模块：
  `lsmod | grep -i "fs\|ext\|xfs\|btrfs"`

- 查找音频模块：
  `lsmod | grep -i "snd\|audio\|sound"`

- 查找 USB 模块：
  `lsmod | grep -i "usb"`

- 查找显卡驱动模块：
  `lsmod | grep -i "drm\|nvidia\|amdgpu\|intel"`

- 查找虚拟化模块：
  `lsmod | grep -i "kvm\|virt\|xen"`

- 查找安全模块：
  `lsmod | grep -i "security\|selinux\|apparmor"`

- 查找加密模块：
  `lsmod | grep -i "crypto\|aes\|sha"`

- 查找存储控制器模块：
  `lsmod | grep -i "sata\|scsi\|raid\|ahci"`

- 查找输入设备模块：
  `lsmod | grep -i "input\|mouse\|keyboard"`

- 查找处理器相关的模块：
  `lsmod | grep -i "cpu\|processor\|intel\|amd"`

- 查找内存管理模块：
  `lsmod | grep -i "memory\|mm\|vmem"`

- 查找调试相关的模块：
  `lsmod | grep -i "debug\|trace"`

- 显示没有被任何模块使用的模块：
  `lsmod | awk '$3 == 0 {print $1}'`

- 显示被多个模块使用的模块：
  `lsmod | awk '$3 > 1 {print $1, $3}'`

- 查找特定模块的依赖关系：
  `lsmod | grep {{模块名}} && modinfo {{模块名}} | grep depends`

- 显示模块的总大小：
  `lsmod | awk 'NR>1 {sum+=$2} END{print "Total size:", sum, "bytes"}'`

- 查找核心系统模块：
  `lsmod | grep -E "(kernel|core|system)"

- 查找硬件驱动模块：
  `lsmod | grep -E "(driver|hw|hardware)"

- 显示模块使用情况统计：
  `lsmod | awk 'NR>1 {used[$3]++} END{for(count in used) print count, "modules used", used[count], "times"}'`

- 查找容器相关的模块：
  `lsmod | grep -i "docker\|container\|cgroup"`

- 查找防火墙模块：
  `lsmod | grep -i "iptables\|netfilter\|firewall"`

- 监控模块变化：
  `watch lsmod`

- 查找模块的依赖树：
  `lsmod | awk '{print $1}' | xargs -I {} sh -c 'echo "=== {} ==="; modinfo {} | grep depends'`

- 显示模块的详细信息：
  `lsmod | awk '{print $1}' | head -10 | xargs -I {} modinfo {}

- 查找特定厂商的模块：
  `lsmod | grep -i "intel\|amd\|nvidia\|broadcom"`

- 显示模块的内存占用：
  `lsmod | awk '{printf "%-20s %10s bytes %10s KB\n", $1, $2, $2/1024}'`

- 查找系统调用相关的模块：
  `lsmod | grep -i "syscall\|system call"`

- 查找进程调度模块：
  `lsmod | grep -i "sched\|schedule"`

- 显示模块的加载顺序：
  `lsmod | awk '{print NR, $1, $2, $3}'`

- 查找网络协议模块：
  `lsmod | grep -i "tcp\|udp\|ipv4\|ipv6"`

- 显示模块的依赖关系图：
  `lsmod | awk 'NR>1 {print $1, "used by:", $3}'`

- 查找内核补丁相关的模块：
  `lsmod | grep -i "patch\|acpi\|firmware"`

- 显示模块的格式化信息：
  `lsmod | column -t`

- 查找时间相关的模块：
  `lsmod | grep -i "time\|clock\|timer"`

- 查找电源管理模块：
  `lsmod | grep -i "power\|battery\|acpi"`

- 显示模块的统计报告：
  `lsmod | awk 'NR>1 {total++; size+=$2; used+=$3} END{print "Total modules:", total; print "Total size:", size, "bytes"; print "Total used:", used, "times"}'`

- 查找内核特性模块：
  `lsmod | grep -i "feature\|capability"`

- 显示模块的详细列表：
  `lsmod && echo "=== Module Details ===" && lsmod | awk 'NR>1 {print "Module:", $1, "Size:", $2, "Used:", $3}'`
