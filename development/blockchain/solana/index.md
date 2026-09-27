# Solana

## 配置管理

### 基础配置

```sh
# 获取当前配置
solana config get

# 设置集群
solana config set --url mainnet-beta
solana config set --url devnet
solana config set --url localhost
solana config set --url testnet

# 设置钱包密钥对
solana config set --keypair ~/.config/solana/dev-wallet.json

# 简写形式
solana config set -um    # mainnet-beta
solana config set -ud    # devnet
solana config set -ul    # localhost
solana config set -ut    # testnet

# 设置 RPC 端点
solana config set --url https://api.mainnet-beta.solana.com
solana config set --url https://api.devnet.solana.com

# 设置超时时间
solana config set --timeout 60
```

### 高级配置 (2024-2025 新增)

```sh
# 设置优先级费用 (Priority Fee)
solana config set --priority-fee 1000

# 设置交易确认策略
solana config set --confirmations finalized

# 启用 JSON 输出格式
solana config set --output json

# 设置 RPC 重试次数
solana config set --retry 3
```

## 钱包管理

### 密钥对操作

```sh
# 生成新的密钥对
solana-keygen new --outfile ~/.config/solana/my-wallet.json

# 从助记词恢复钱包
solana-keygen recover -o ~/.config/solana/recovered-wallet.json

# 显示钱包地址
solana address
solana address --keypair ~/.config/solana/my-wallet.json

# 显示钱包余额
solana balance
solana balance --keypair ~/.config/solana/my-wallet.json
solana balance ADDRESS --url devnet

# 检查钱包是否为空
solana balance --keypair ~/.config/solana/my-wallet.json --zero
```

### 空投和转账

```sh
# 请求空投 (devnet/testnet)
solana airdrop 2
solana airdrop 10 --url devnet
solana airdrop 0.5 --url testnet

# 批量空投 (2024 新增)
solana airdrop --from-file addresses.txt 1

# 转账
solana transfer DST_ADDRESS AMOUNT
solana transfer DST_ADDRESS AMOUNT --url devnet
solana transfer DST_ADDRESS AMOUNT --allow-unfunded-recipient

# 带备注的转账
solana transfer DST_ADDRESS AMOUNT --with-memo "Payment for services"

# 设置优先级费用的转账 (2024 新增)
solana transfer DST_ADDRESS AMOUNT --priority-fee 5000
```

## 程序管理

### 程序部署

```sh
# 部署程序
solana program deploy ./target/deploy/my_program.so

# 部署到特定集群
solana program deploy ./target/deploy/my_program.so --url devnet

# 部署时指定升级权限
solana program deploy ./target/deploy/my_program.so --upgrade-authority my-wallet.json

# 部署到特定程序地址
solana program deploy ./target/deploy/my_program.so --program-id PROGRAM_ID.json

# 部署时设置缓冲区
solana program deploy ./target/deploy/my_program.so --buffer BUFFER_KEYPAIR.json
```

### 程序信息查询

```sh
# 显示程序详情
solana program show PROGRAM_ID
solana program show PROGRAM_ID --url devnet

# 列出所有程序
solana program list
solana program list --url devnet

# 检查程序是否可升级
solana program is-upgradeable PROGRAM_ID

# 获取程序数据
solana program data PROGRAM_ID --output-file program_data.bin
```

### 程序升级和管理

```sh
# 升级程序
solana program deploy ./target/deploy/updated_program.so --program-id EXISTING_PROGRAM_ID

# 关闭程序账户 (回收 SOL)
solana program close PROGRAM_ID
solana program close PROGRAM_ID --recipient RECIPIENT_ADDRESS

# 设置程序升级权限
solana program set-upgrade-authority PROGRAM_ID --new-upgrade-authority NEW_AUTHORITY.json

# 冻结程序 (2024 新增)
solana program freeze PROGRAM_ID

# 解冻程序 (2024 新增)
solana program unfreeze PROGRAM_ID
```

## 账户管理

### 账户查询

```sh
# 获取账户信息
solana account PUBLIC_KEY
solana account PUBLIC_KEY --output json
solana account PUBLIC_KEY --url devnet

# 获取多个账户信息
solana account --output json ADDRESS1 ADDRESS2 ADDRESS3

# 获取账户数据 (Base64 编码)
solana account PUBLIC_KEY --output base64

# 获取账户数据 (十六进制)
solana account PUBLIC_KEY --output hex
```

### 账户创建

```sh
# 创建系统账户
solana create-address-with-seed BASE_ADDRESS SEED_STRING PROGRAM_ID

# 创建带资金的账户
solana transfer NEW_ADDRESS 0 --allow-unfunded-recipient --from EXISTING_ADDRESS

# 创建 PDA (Program Derived Address)
solana resolve-signer PDA_SEED --program-id PROGRAM_ID
```

## 交易管理

### 交易操作

```sh
# 发送签名交易
solana send-and-confirm-tx SIGNED_TRANSACTION_FILE.json

# 获取交易状态
solana confirm TRANSACTION_SIGNATURE
solana confirm TRANSACTION_SIGNATURE --url devnet

# 获取交易详情
solana transaction-confirmation TRANSACTION_SIGNATURE
solana transaction-confirmation TRANSACTION_SIGNATURE --output json

# 获取最近的交易
solana transaction-history ADDRESS
solana transaction-history ADDRESS --limit 10
```

### 交易构建 (2024-2025 新增)

```sh
# 构建离线交易
solana offline-transaction build --from FROM_ADDRESS --to TO_ADDRESS --amount 1.0

# 签名离线交易
solana offline-transaction sign --keypair KEYPAIR.json --transaction-file tx.json

# 广播离线交易
solana offline-transaction broadcast --transaction-file signed_tx.json
```

## 网络和集群

### 集群信息

```sh
# 获取集群信息
solana cluster-version
solana cluster-version --url devnet

# 获取 Slot 信息
solana slot
solana slot --url devnet

# 获取纪元信息
solana epoch-info
solana epoch-info --url devnet

# 获取最近的区块哈希
solana recent-blockhash
solana recent-blockhash --url devnet
```

### 网络状态

```sh
# 获取网络统计
solana gossip
solana gossip --url devnet

# 获取验证器信息
solana validators
solana validators --url devnet
solana validators --output json

# 获取活跃节点
solana gossip --url devnet --active-stake
```

## 代币和 SPL 代币

### SPL 代币操作

```sh
# 创建代币 Mint
spl-token create-token

# 创建代币账户
spl-token create-account TOKEN_MINT_ADDRESS

# 铸造代币
spl-token mint TOKEN_MINT_ADDRESS 1000

# 转移代币
spl-token transfer TOKEN_MINT_ADDRESS 100 DESTINATION_ADDRESS

# 冻结代币账户
spl-token freeze ACCOUNT_ADDRESS

# 解冻代币账户
spl-token thaw ACCOUNT_ADDRESS

# 关闭代币账户
spl-token close ACCOUNT_ADDRESS
```

### 代币信息查询

```sh
# 获取代币余额
spl-token balance TOKEN_MINT_ADDRESS
spl-token balance TOKEN_MINT_ADDRESS --address ACCOUNT_ADDRESS

# 列出代币账户
spl-token accounts
spl-token accounts TOKEN_MINT_ADDRESS

# 获取代币供应量
spl-token supply TOKEN_MINT_ADDRESS
```

## 质押管理

### 质押操作

```sh
# 创建质押账户
solana create-stake-account STAKE_ACCOUNT_KEYPAIR.json 1

# 委托质押
solana delegate-stake STAKE_ACCOUNT_ADDRESS VALIDATOR_VOTE_ACCOUNT_ADDRESS

# 取消委托
solana deactivate-stake STAKE_ACCOUNT_ADDRESS

# 提取质押资金
solana withdraw-stake STAKE_ACCOUNT_ADDRESS DESTINATION_ADDRESS AMOUNT

# 合并质押账户
solana merge-stake SOURCE_STAKE_ACCOUNT DESTINATION_STAKE_ACCOUNT
```

### 质押信息查询

```sh
# 获取质押账户信息
solana stake-account STAKE_ACCOUNT_ADDRESS
solana stake-account STAKE_ACCOUNT_ADDRESS --url devnet

# 获取验证器信息
solana vote-account VALIDATOR_VOTE_ACCOUNT_ADDRESS
solana vote-account VALIDATOR_VOTE_ACCOUNT_ADDRESS --url devnet

# 获取活跃质押信息
solana vote-account VALIDATOR_VOTE_ACCOUNT_ADDRESS --lamports
```

## 高级功能

### 事件和日志

```sh
# 监控日志
solana logs
solana logs ADDRESS
solana logs --url devnet

# 获取程序日志
solana logs PROGRAM_ID --program-log-level debug
```

### 性能监控

```sh
# 获取 RPC 性能统计
solana rpc-url --url devnet --show-stats

# 测试 RPC 延迟
solana ping --url devnet --count 10

# 获取网络延迟
solana ping --url devnet --delay 1000
```

### 批量操作

```sh
# 批量转账 (2024 新增)
solana bulk-transfer --from-file transfers.csv

# 批量空投 (2024 新增)
solana bulk-airdrop --from-file addresses.csv 1

# 批量程序部署
solana bulk-deploy --from-file programs.json
```

## 开发工具

### 本地开发

```sh
# 启动本地测试验证器
solana-test-validator

# 重置本地验证器
solana-test-validator --reset

# 使用自定义配置启动验证器
solana-test-validator --ledger ./ledger --rpc-port 8899

# 导入账户到测试验证器
solana-test-validator --account ADDRESS FILE.json
```

### 调试工具

```sh
# 获取交易执行详情
solana transaction-status TRANSACTION_SIGNATURE --verbose

# 模拟交易
solana simulate-transaction TRANSACTION_FILE.json

# 获取账户变更
solana account-changes ACCOUNT_ADDRESS
```

## 安全功能

### 密钥管理

```sh
# 生成安全的密钥对
solana-keygen new --force --no-outfile

# 验证密钥对
solana-keygen verify PUBLIC_KEY FILE.json

# 生成助记词
solana-keygen new --no-outfile --word-count 24
```

### 交易安全

```sh
# 设置交易超时
solana config set --timeout 120

# 启用交易确认
solana config set --confirm

# 设置最大费用
solana config set --max-fee 0.000005
```

## 输出格式

### 格式选项

```sh
# JSON 格式输出
solana account ADDRESS --output json

# CSV 格式输出
solana account ADDRESS --output csv

# 表格格式输出 (默认)
solana account ADDRESS --output table

# 机器可读格式
solana account ADDRESS --output short
```

## 故障排除

### 常见问题解决

```sh
# 检查网络连接
solana ping --url devnet

# 检查钱包配置
solana config get

# 清除缓存
solana cache clear

# 重置配置
solana config reset
```

### 调试选项

```sh
# 启用详细输出
solana --verbose command

# 启用调试模式
solana --log-level debug command

# 显示执行时间
solana --timing command
```

## 最佳实践

### 安全建议

1. **密钥管理**: 始终备份助记词，不要分享私钥
2. **网络选择**: 开发时使用 devnet，生产前在 testnet 测试
3. **费用管理**: 设置合理的优先级费用避免交易失败
4. **确认策略**: 生产环境使用 `finalized` 确认级别
5. **批量操作**: 大量操作时使用批量命令提高效率

### 性能优化

1. **RPC 选择**: 使用响应快的 RPC 节点
2. **并发控制**: 避免同时发送过多交易
3. **缓存利用**: 合理使用本地缓存减少网络请求
4. **批量处理**: 使用批量命令处理大量数据

## 资源链接

- [官方文档](https://docs.solana.com/cli)
- [Solana CLI 源码](https://github.com/solana-labs/solana/tree/master/cli)
- [SPL 代币工具](https://spl.solana.com/token)
- [开发工具指南](https://docs.solana.com/developing/clients)
