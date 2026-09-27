# firewalld

## zone 的概念

firewalld 最核心的概念就是 区域 (Zone)。你可以把它想象成对网络连接的“信任等级”。你的电脑可能同时连接着好几个网络（比如有线网卡、Wi-Fi、虚拟机网卡），你以给每个网络接口分配一个区域，从而应用不同的安全策略。

常用的几个默认区域：

- public: 完全不信任网络里的其他人
- home: 家庭网络
- work: 工作网络
- internal: 内部网络
- external: 外部网络
- block: 丢弃入方向的包，但是会明确拒绝连接
- drop: 最低信任等级，所有入方向的包都将被直接丢弃，并且无应答

## 运行时配置 & 永久配置

运行时: 你现在做的修改立刻生效，但电脑重启后就没了。这非常适合用来临时测试！

永久: 修改会保存到配置文件里，重启后依然有效。

如果你想让一个规则永久生效，只需要在命令后面加上 `--permanent` 就行了。

## 常用操作

```sh
# 查看当前防火墙状态
sudo firewall-cmd --state

# 查看所有区域的配置
sudo firewall-cmd --list-all-zones

# 查看默认区域
sudo firewall-cmd --get-default-zone

# 查看当前生效的区域（和它绑定的网卡）
sudo firewall-cmd --get-active-zones

# 查看 public 区域的所有规则
sudo firewall-cmd --zone=public --list-all

# 把 eth0 网卡接口绑定到 internal 区域
sudo firewall-cmd --zone=internal --change-interface=eth0

# 修改默认区域为 home
sudo firewall-cmd --set-default-zone=home
```

## 开放/关闭端口和服务

```sh
# 查看所有预设的服务
firewall-cmd --get-services

# 临时开放 http 服务
sudo firewall-cmd --zone=public --add-service=http

# 永久开放 http 服务
sudo firewall-cmd --zone=public --add-service=http --permanent

# 临时开放 TCP 8000 端口
sudo firewall-cmd --zone=public --add-port=8000/tcp

# 永久开放 TCP 8000 端口
sudo firewall-cmd --zone=public --add-port=8000/tcp --permanent

# 别忘了！修改了 --permanent 规则后，需要重载防火墙才能生效
sudo firewall-cmd --reload

# 查看 public 区域当前开放的服务和端口
sudo firewall-cmd --zone=public --list-services
sudo firewall-cmd --zone=public --list-ports

# 临时移除 http 服务
sudo firewall-cmd --zone=public --remove-service=http

# 永久移除 TCP 8000 端口
sudo firewall-cmd --zone=public --remove-port=8000/tcp --permanent
```
