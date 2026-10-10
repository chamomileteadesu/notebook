# Solana Keygen

## 基础用法

### 生成密钥对

```sh
# 在默认密钥对路径生成一个密钥对
solana-keygen new --outfile ~/.config/solana/dev-wallet.json

# 生成密钥对但不保存到文件 (仅显示)
solana-keygen new --no-outfile

# 生成指定字数的助记词
solana-keygen new --word-count 24

# 生成密钥对并显示详细信息
solana-keygen new --outfile wallet.json --verbose

# 强制覆盖现有文件
solana-keygen new --outfile existing.json --force
```

### 从助记词恢复钱包

```sh
# 从助记词恢复钱包
solana-keygen recover -o ~/.config/solana/recovered-wallet.json

# 从特定索引恢复 HD 钱包
solana-keygen recover -o wallet.json --hd-path "m/44'/501'/0'/0'/0'"

# 从自定义路径恢复
solana-keygen recover -o wallet.json --hd-path "m/44'/501'/1'/0'/0'"
```

### 密钥验证

```sh
# 验证密钥对文件
solana-keygen verify PUBLIC_KEY wallet.json

# 验证助记词
solana-keygen verify PUBLIC_KEY --phrase-file phrase.txt

# 检查密钥对是否有效
solana-keygen verify PUBLIC_KEY --no-outfile
```

## 高级功能

### 密钥生成优化 (2024-2025 新增)

```sh
# 生成带有特定前缀的地址 (优化版本)
solana-keygen grind --starts-with myprefix:4 --threads 8

# 生成带有特定后缀的地址
solana-keygen grind --ends-with suffix:2

# 生成包含特定字符串的地址
solana-keygen grind --include-string "SOLANA"

# 生成不包含特定字符的地址 (提高可读性)
solana-keygen grind --exclude-chars "0O1lI"

# 生成多个匹配的地址
solana-keygen grind --starts-with prefix:3 --count 5
```

### 批量密钥生成

```sh
# 批量生成密钥对
solana-keygen batch-new --count 10 --output-dir ./wallets/

# 生成带标签的密钥对
solana-keygen new --outfile wallet.json --label "Development Wallet"

# 生成用于测试的密钥对集合
solana-keygen batch-new --count 100 --output-dir ./test-wallets/ --test-mode
```

### 安全增强功能

```sh
# 生成高强度密钥对 (使用更强的随机源)
solana-keygen new --strong --outfile secure-wallet.json

# 生成离线密钥对 (不连接网络)
solana-keygen new --offline --outfile offline-wallet.json

# 生成带时间戳的密钥对
solana-keygen new --timestamp --outfile timestamped-wallet.json
```

## 安全最佳实践

### 1. 密钥生成安全

```sh
# 在离线环境中生成密钥对
solana-keygen new --offline --outfile cold-wallet.json

# 使用硬件随机数生成器 (如果可用)
solana-keygen new --hardware-rng --outfile hw-wallet.json

# 生成后立即设置文件权限
chmod 600 ~/.config/solana/wallet.json
```

### 2. 助记词管理

```sh
# 生成助记词并保存到安全位置
solana-keygen new --no-outfile --word-count 24 > mnemonic.txt
chmod 600 mnemonic.txt

# 从文件恢复助记词
solana-keygen recover -o wallet.json --phrase-file mnemonic.txt
```

### 3. 多重签名支持

```sh
# 生成多重签名钱包的各个密钥
solana-keygen new --outfile key1.json
solana-keygen new --outfile key2.json
solana-keygen new --outfile key3.json

# 创建多重签名地址
solana create-multisig 2 key1.json key2.json key3.json
```

### 4. 硬件钱包集成

```sh
# 与 Ledger 设备集成
solana-keygen ledger new --outfile ledger-wallet.json

# 验证 Ledger 设备连接
solana-keygen ledger verify --device-path /dev/hidraw0

# 从 Ledger 恢复钱包
solana-keygen ledger recover --outfile ledger-wallet.json
```

## 地址美化 (Address Beautification)

### grind 命令详解

```sh
# 基础用法
solana-keygen grind --starts-with prefix:3

# 参数说明
--starts-with PREFIX:LENGTH    # 地址以指定前缀开始
--ends-with SUFFIX:LENGTH      # 地址以指定后缀结束
--include-string STRING        # 地址包含指定字符串
--exclude-chars CHARS          # 排除特定字符
--threads N                    # 使用的线程数
--count N                      # 生成匹配地址的数量
--timeout SECONDS             # 最大等待时间
```

### 实用的 grind 示例

```sh
# 生成以 "SOL" 开头的地址 (3个字符)
solana-keygen grind --starts-with SOL:3

# 生成以特定用户名开头的地址
solana-keygen grind --starts-with chamomile:9

# 生成易于识别的地址 (避免混淆字符)
solana-keygen grind --starts-with SAFE:4 --exclude-chars "0O1lI"

# 生成包含项目名称的地址
solana-keygen grind --include-string "PROJECT" --count 3

# 快速生成 (使用更多线程)
solana-keygen grind --starts-with DEV:3 --threads 16
```

## 密钥管理策略

### 1. 开发环境密钥管理

```sh
# 为不同环境创建不同的密钥对
solana-keygen new --outfile ~/.config/solana/dev-wallet.json
solana-keygen new --outfile ~/.config/solana/test-wallet.json
solana-keygen new --outfile ~/.config/solana/staging-wallet.json
```

### 2. 生产环境密钥管理

```sh
# 创建主钱包和备份钱包
solana-keygen new --outfile ~/.config/solana/main-wallet.json
solana-keygen new --outfile ~/.config/solana/backup-wallet.json

# 设置适当的文件权限
chmod 600 ~/.config/solana/main-wallet.json
chmod 600 ~/.config/solana/backup-wallet.json

# 创建密钥备份
cp ~/.config/solana/main-wallet.json ~/.config/solana/main-wallet.json.backup
gpg --encrypt --recipient your-email@example.com ~/.config/solana/main-wallet.json
```

### 3. 团队密钥管理

```sh
# 为团队成员生成密钥对
solana-keygen new --outfile ./team/alice.json
solana-keygen new --outfile ./team/bob.json
solana-keygen new --outfile ./team/charlie.json

# 创建团队多重签名钱包
solana create-multisig 2 ./team/alice.json ./team/bob.json ./team/charlie.json
```

## 故障排除

### 常见问题解决

```sh
# 检查密钥文件格式
solana-keygen verify PUBLIC_KEY wallet.json

# 重新生成损坏的密钥对
rm ~/.config/solana/wallet.json
solana-keygen new --outfile ~/.config/solana/wallet.json

# 检查助记词有效性
solana-keygen recover -o test.json --phrase-file mnemonic.txt
```

### 性能优化

```sh
# 使用更多线程加速 grind 过程
solana-keygen grind --starts-with PREFIX:3 --threads $(nproc)

# 限制内存使用
solana-keygen grind --starts-with PREFIX:3 --memory-limit 2G

# 设置超时避免无限等待
solana-keygen grind --starts-with PREFIX:3 --timeout 3600
```

## 安全建议总结

### 1. 密钥生成阶段
- 在离线环境中生成密钥对
- 使用强随机数生成器
- 记录生成时间和环境

### 2. 密钥存储阶段
- 使用加密存储 (如 GPG)
- 多地备份但控制访问权限
- 定期检查备份完整性

### 3. 密钥使用阶段
- 生产环境使用硬件钱包
- 开发环境使用独立的密钥对
- 定期轮换开发密钥

### 4. 密钥销毁阶段
- 安全删除不再使用的密钥
- 清理系统日志中的敏感信息
- 更新相关的访问控制列表

## 监控和审计

```sh
# 监控密钥使用情况
solana-keygen audit --wallet wallet.json --output audit.log

# 检查密钥安全性
solana-keygen security-check --wallet wallet.json

# 生成密钥使用报告
solana-keygen report --wallet wallet.json --output report.json
```

## 资源链接

- [Solana 官方安全指南](https://docs.solana.com/wallet-guide)
- [密钥管理最佳实践](https://solanacookbook.com/core-wallets/keypairs.html)
- [多重签名钱包文档](https://docs.solana.com/wallet-guide/paper-wallet#multisig-paper-wallet)
- [硬件钱包集成](https://docs.solana.com/wallet-guide/hardware-wallets)
