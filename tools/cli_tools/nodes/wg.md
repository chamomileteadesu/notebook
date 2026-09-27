# wg

## 安装 wireguard

```shell
# 安装相关软件
sudo apt install wireguard resolvconf
# 开启 IP 转发
echo 'net.ipv4.ip_forward = 1' | sudo tee -a /etc/sysctl.conf
# 调整 wireguard 目录权限
cd /etc/wireguard
chmod 0777 /etc/wireguard
umask 077
```

## 生成服务器密钥对

```shell
# 生成私钥
wg genkey > server.key
# 通过私钥生成公钥
wg pubkey < server.key > server.key.pub
```

## 创建服务器配置文件

wg0.conf:

```toml
[Interface]
Address = 10.13.13.1/24      # WG 服务器地址，同时指明了 VPN 网段
ListenPort = 51820           # WG 服务端口
PrivateKey = PK              # WG-sererver 私钥
PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -A FORWARD -o %i -j ACCEPT; iptables -t nat -A POSTROUTING -o eth+ -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -D FORWARD -o %i -j ACCEPT; iptables -t nat -D POSTROUTING -o eth+ -j MASQUERADE

[Peer]
# peer1
# peer1 的公钥
PublicKey = rJcgI+g5dEjbCREA8mgnZsgR0jHe7XZ5p0+pkL/szzA=
# 与 peer1 的预共享密钥，可选
PresharedKey = FQvI7f1NBHIjBhlKi9NOuapHPTqwpTrWQz1mr1wyoD4=
# peer1 的地址
AllowedIPs = 10.13.13.2/32

[Peer]
# peer2
PublicKey = yr764qeCq7OGq2pAkD5z3sg/obaU8BBmVkUrhQsn9VY=
PresharedKey = ZqyTd7WLRw/nAKQISnFbmqr1ir40Vhj3ZWLfNGZym1o=
AllowedIPs = 10.13.13.3/32
```

## 启动服务端 wireguard

```shell
# 启动
wg-quick up wg0
# 关闭
wg-quick down wg0
```

## 生成客户端密钥对

```shell
# 生成私钥
wg genkey > client1.key
# 通过私钥生成公钥
wg pubkey < client1.key > client1.key.pub
```

## 客户端 client 的配置

```toml
[Interface]
Address = 10.13.13.2/32            # 客户端在 VPN 内的 IP
PrivateKey = c1ient-pri-key        # 客户端公钥
DNS = 8.8.8.8
MTU = 1500

[Peer]
PublicKey = server-pub-key         # WG-server 的公钥
PresharedKey = PRESHAREDKEY        # 与服务器的预共享密钥
Endpoint = SERVER_IP:SERVER_PORT   # WG-server 端点
AllowedIPs = 10.13.13.0/24         # 这个网段的流量将通过隧道
```
