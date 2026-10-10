# lspci

> 显示 PCI 总线信息和连接的设备。
> 更多信息：<https://manned.org/lspci>

- 显示所有 PCI 设备的简洁列表：
  `lspci`

- 以详细格式显示 PCI 设备：
  `lspci -v`

- 以更详细的格式显示设备：
  `lspci -vv`

- 显示设备的数值代码：
  `lspci -n`

- 显示十六进制的设备地址：
  `lspci -D`

- 显示设备的内核驱动：
  `lspci -k`

- 按设备类型分类显示：
  `lspci -d {{设备类型}}`

- 显示 PCI 设备树：
  `lspci -t`

- 查找特定厂商的设备：
  `lspci | grep {{厂商名}}`

- 查找特定设备 ID：
  `lspci -d {{供应商ID}}:{{设备ID}}`

- 显示显卡信息：
  `lspci | grep -i "vga\|3d\|display"`

- 显示网络设备：
  `lspci | grep -i "ethernet\|network"`

- 显示存储控制器：
  `lspci | grep -i "sata\|scsi\|raid"`

- 显示音频设备：
  `lspci | grep -i "audio\|sound"`

- 显示 USB 控制器：
  `lspci | grep -i "usb"`

- 查找 PCIe 设备：
  `lspci | grep -i "pci express"`

- 显示设备的详细信息包括驱动：
  `lspci -v -k`

- 查找特定功能的设备：
  `lspci -d ::{{设备类}}`

- 显示设备的总线 ID：
  `lspci -D | grep {{设备名}}`

- 查找多媒体设备：
  `lspci | grep -i "multimedia\|video"`

- 显示桥接设备：
  `lspci | grep -i "bridge"`

- 查找加密设备：
  `lspci | grep -i "crypto\|security"`

- 显示设备的内存映射：
  `lspci -v | grep -A 5 "Region"`

- 查找通信设备：
  `lspci | grep -i "communication"`

- 显示设备的 IRQ 信息：
  `lspci -v | grep -i "irq"`

- 查找输入设备：
  `lspci | grep -i "input\|human interface"`

- 显示设备的电源管理：
  `lspci -v | grep -i "power"`

- 查找处理器的 PCI 接口：
  `lspci | grep -i "host bridge\|processor"`

- 显示设备的速度信息：
  `lspci -v | grep -i "width\|speed"`

- 查找基板设备：
  `lspci | grep -i "base system"`

- 显示设备的内存大小：
  `lspci -v | grep -A 3 "Memory at"`

- 查找传感器设备：
  `lspci | grep -i "sensor"`

- 显示设备的版本信息：
  `lspci -v | grep -i "revision"`

- 查找 Co-处理器：
  `lspci | grep -i "co-processor"`

- 显示设备的子系统信息：
  `lspci -v | grep -A 2 "Subsystem"`

- 查找卫星通信设备：
  `lspci | grep -i "satellite"`

- 显示设备的配置寄存器：
  `lspci -vv | grep -A 10 "Config"

- 查找工业自动化设备：
  `lspci | grep -i "industrial"`

- 显示设备的中断向量：
  `lspci -v | grep -i "interrupt"`

- 查找电信设备：
  `lspci | grep -i "telecom"`

- 显示设备的扩展功能：
  `lspci -vv | grep -A 5 "Capabilities"`

- 查找测量设备：
  `lspci | grep -i "measurement"`

- 显示设备的链路状态：
  `lspci -v | grep -i "link"`

- 查找机器人设备：
  `lspci | grep -i "robotics"`

- 显示设备的时钟信息：
  `lspci -vv | grep -i "clock"`

- 查找运动控制设备：
  `lspci | grep -i "motion"`

- 显示设备的调试信息：
  `lspci -vvv`

- 查找医学设备：
  `lspci | grep -i "medical"`

- 显示设备的 DMA 通道：
  `lspci -v | grep -i "dma"`

- 查找实验设备：
  `lspci | grep -i "experimental"`

- 显示设备的缓存信息：
  `lspci -vv | grep -i "cache"`

- 查找军用设备：
  `lspci | grep -i "military"`

- 显示设备的测试模式：
  `lspci -vv | grep -i "test"`

- 查找航空航天设备：
  `lspci | grep -i "aerospace"`

- 显示设备的错误信息：
  `lspci -v | grep -i "error"`