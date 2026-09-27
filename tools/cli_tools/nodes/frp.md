# frp

- 需要一台公网服务器
- client使用 frpc，server 使用 frps

## 服务端

### 服务端配置文件

```toml
# frps.toml
# 服务器监听 bindPort 等待客户端连接
# 确保防火墙放行了这个端口
bindPort = 7000
# 可选：服务端设置的认证 token
auth.token = "a_complex_password"
```

### 服务端启动服务

```sh
# -c: --config
frps -c frps.toml
```

### 将 frps 注册为系统服务

```sh
# 让程序能够从环境变量中被找到
cp frps /usr/local/bin
# 存放配置文件
mkdir /etc/frp
cp frps.toml /etc/frp
# 创建一个新的服务单元
sudo vi /etc/systemd/system/frps.service
# 编写 frps.service，然后执行：
sudo systemctl daemon-reload
```

frps.service:

```toml
[Unit]
Description=frp Server Service
After=network.target  # 表示这个服务应该在网络准备好之后再启动

[Service]
Type=simple
User=nobody  # 使用一个低权限用户运行更安全
Restart=on-failure  # 如果 frps 异常退出了，systemd 会自动尝试在 RestartRec 后重启它
RestartSec=5s
ExecStart=/usr/local/bin/frps -c /etc/frp/frps.toml  # 这里要写绝对路径

[Install]
WantedBy=multi-user.target
```

## 客户端

### 客户端配置文件

```toml
# frpc.toml
serverAddr = "x.x.x.x"      # 公网服务器 IP 地址
serverPort = 7000           # 和 frps 的 bindPort 保持一致

[[proxies]]
name = "my-web-app"         # 代理规则的名字，随便取，方便自己识别
type = "http"               # 代理类型
localIP = "127.0.0.1"       # 本地服务的 IP 地址，通常就是 127.0.0.1
localPort = 8000            # 本地服务的端口号
remotePort = 8080           # 访问公网服务器的这个端口，就会转发到你的本地服务，服务器防火墙要放行这个端口
auth.token = "pwd"          # 必须与服务器设置的 token 一致才能访问
```

### 运行客户端

```sh
frpc -c frpc.ini
```
