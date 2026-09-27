# Qemu

## 安装 qemu

```sh
sudo apt install qemu-system qemu-user qemu-efi virt-manager
```

## 磁盘镜像管理

```sh
# 创建磁盘镜像
# -f: 指定磁盘镜像格式
qemu-img create -f qcow2 disk.qcow2 10G

# 查看磁盘信息
qemu-img info disk.qcow2

# 磁盘镜像格式转换
# 将 qcow2 格式转化为 raw（还支持 vmdk、vdi 等）
qemu-img convert -f qcow2 -O raw disk.qcow2 disk.raw

# 调整磁盘大小
qemu-img resize disk.qcow2 +10G

# 快照管理
# 创建快照
qemu-img snapshot -c snapshot1 disk.img
# 列出快照
qemu-img snapshot -l disk.img
# 回滚到快照
qemu-img snapshot -a snapshot1 disk.img
```

## 系统级虚拟

```sh
qemu-system-x86_64 \
-smp 2 \               # CPU 核心数
-m 2G \                # 分配内存
-hda disk.img \        # 使用 disk.img 作为主硬盘
-cdrom debian.iso      # -cdrom debian.iso: 挂载 ISO 镜像作为光驱
-enable-kvm            #  启用 KVM 加速（需硬件支持）
# -boot <d/c>
# -vga std: 启用标准图形输出
# -net nic -net user: 启用网络（NAT 模式）
# -net user,hostfwd=tcp::2222-:22 -net nic  ：端口转发（将主机端口映射到虚拟机）
```
