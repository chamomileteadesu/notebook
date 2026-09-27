# lsusb

> 显示 USB 总线信息和连接的设备。
> 更多信息：<https://manned.org/lsusb>

- 显示所有 USB 设备：
  `lsusb`

- 以详细格式显示 USB 设备：
  `lsusb -v`

- 显示 USB 设备树结构：
  `lsusb -t`

- 显示特定设备的详细信息：
  `lsusb -v -s {{总线号}}:{{设备号}}`

- 按供应商 ID 和产品 ID 查找设备：
  `lsusb -d {{供应商ID}}:{{产品ID}}`

- 显示设备名称和序列号：
  `lsusb -v | grep -E "(iManufacturer|iProduct|iSerial)"`

- 查找特定厂商的 USB 设备：
  `lsusb | grep {{厂商名}}`

- 显示 USB 设备的功率信息：
  `lsusb -v | grep -E "(MaxPower|Bus|Device)"`

- 显示 USB 控制器信息：
  `lsusb -v | grep -A 5 "Host Controller"`

- 查找大容量存储设备：
  `lsusb | grep -i "mass storage"`

- 查找 USB 网络设备：
  `lsusb | grep -i "ethernet\|wireless"`

- 查找 USB 音频设备：
  `lsusb | grep -i "audio"`

- 查找 USB 摄像头设备：
  `lsusb | grep -i "camera\|video"`

- 显示 USB 设备的驱动信息：
  `lsusb -t | grep -E "(Driver|usb)"`

- 查找 USB 调制解调器：
  `lsusb | grep -i "modem"`

- 显示 USB 设备的版本信息：
  `lsusb -v | grep -E "(bcdUSB|bcdDevice|bcdUSB)"`

- 查找 USB 蓝牙适配器：
  `lsusb | grep -i "bluetooth"`

- 显示 USB 设备的配置描述符：
  `lsusb -v | grep -A 20 "Configuration Descriptor"`

- 查找 USB 串口设备：
  `lsusb | grep -i "serial\|uart"`

- 显示 USB 设备的接口信息：
  `lsusb -v | grep -A 10 "Interface Descriptor"`

- 查找 USB 打印机：
  `lsusb | grep -i "printer"`

- 显示 USB 设备的端点信息：
  `lsusb -v | grep -A 5 "Endpoint"`

- 查找 USB 读卡器：
  `lsusb | grep -i "card reader"`

- 显示 USB 设备的语言 ID：
  `lsusb -v | grep "LangID"`

- 查找 USB 键盘设备：
  `lsusb | grep -i "keyboard"`

- 显示 USB 设备的设备类：
  `lsusb -v | grep "bDeviceClass"`

- 查找 USB 鼠标设备：
  `lsusb | grep -i "mouse"`

- 显示 USB 设备的协议：
  `lsusb -v | grep "bDeviceProtocol"`

- 查找 USB 游戏手柄：
  `lsusb | grep -i "game\|joystick"`

- 显示 USB 设备的子类：
  `lsusb -v | grep "bDeviceSubClass"`

- 查找 USB GPS 设备：
  `lsusb | grep -i "gps"`

- 显示 USB 设备的包大小：
  `lsusb -v | grep "wMaxPacketSize"`

- 查找 USB 指纹识别器：
  `lsusb | grep -i "fingerprint"`

- 显示 USB 设备的间隔时间：
  `lsusb -v | grep "bInterval"`

- 查找 USB 加密狗：
  `lsusb | grep -i "dongle\|key"`

- 显示 USB 设备的供应商名称：
  `lsusb -v | grep "iManufacturer"`

- 查找 USB 扫描仪：
  `lsusb | grep -i "scanner"`

- 显示 USB 设备的产品名称：
  `lsusb -v | grep "iProduct"`

- 查找 USB 显示器：
  `lsusb | grep -i "display\|monitor"`

- 显示 USB 设备的序列号：
  `lsusb -v | grep "iSerial"`

- 查找 USB 硬盘：
  `lsusb | grep -i "disk\|hdd"`

- 显示 USB 设备的总线速度：
  `lsusb -v | grep -E "(bcdUSB|Speed)"`

- 查找 USB 转串口适配器：
  `lsusb | grep -i "adapter\|converter"`

- 监控 USB 设备的连接/断开：
  `watch lsusb`

- 查找 USB 无线网卡：
  `lsusb | grep -i "wireless\|wifi"`

- 显示 USB 设备的电源管理信息：
  `lsusb -v | grep -E "(Power|Remote)"`

- 查找 USB 手机连接设备：
  `lsusb | grep -i "phone\|mobile"`

- 显示 USB 设备的物理连接：
  `lsusb -t | grep -E "(Port|Dev)"`

- 查找 USB 虚拟化设备：
  `lsusb | grep -i "virtual\|vm"`