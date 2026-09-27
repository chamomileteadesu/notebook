# SPL Token 工具

## 概述

SPL Token 是 Solana 生态系统中的标准代币标准，类似于以太坊的 ERC-20。SPL Token CLI 工具提供了创建、管理和交互各种代币的完整功能。

## 安装

```sh
# 通过 Cargo 安装
cargo install spl-token-cli

# 验证安装
spl-token --version
```

## 基础操作

### 1. 创建代币 Mint

```sh
# 创建新的代币 Mint
spl-token create-token

# 创建指定小数位的代币
spl-token create-token --decimals 6

# 创建不可冻结的代币
spl-token create-token --enable-freeze

# 创建带标签的代币
spl-token create-token --name "My Token" --symbol "MTK" --description "My Custom Token"
```

### 2. 创建代币账户

```sh
# 为当前钱包创建代币账户
spl-token create-account TOKEN_MINT_ADDRESS

# 为指定地址创建代币账户
spl-token create-account TOKEN_MINT_ADDRESS --owner DESTINATION_ADDRESS

# 创建带标签的代币账户
spl-token create-account TOKEN_MINT_ADDRESS --name "My Token Account"
```

### 3. 铸造代币

```sh
# 铸造代币到默认账户
spl-token mint TOKEN_MINT_ADDRESS 1000

# 铸造代币到指定账户
spl-token mint TOKEN_MINT_ADDRESS 1000 DESTINATION_ACCOUNT

# 铸造指定小数位的代币
spl-token mint TOKEN_MINT_ADDRESS 100.5
```

### 4. 转移代币

```sh
# 转移代币
spl-token transfer SOURCE_ACCOUNT 100 DESTINATION_ACCOUNT

# 带备注的转移
spl-token transfer SOURCE_ACCOUNT 100 DESTINATION_ACCOUNT --memo "Payment for services"

# 允许未资金账户接收代币
spl-token transfer SOURCE_ACCOUNT 100 DESTINATION_ACCOUNT --allow-unfunded-recipient
```

## 高级功能

### 1. 代币管理

```sh
# 冻结代币账户
spl-token freeze ACCOUNT_ADDRESS

# 解冻代币账户
spl-token thaw ACCOUNT_ADDRESS

# 关闭代币账户 (回收 SOL)
spl-token close ACCOUNT_ADDRESS

# 关闭代币账户并指定接收地址
spl-token close ACCOUNT_ADDRESS --recipient RECEIVING_ACCOUNT
```

### 2. 代币信息查询

```sh
# 获取代币余额
spl-token balance TOKEN_MINT_ADDRESS
spl-token balance TOKEN_MINT_ADDRESS --address ACCOUNT_ADDRESS

# 列出所有代币账户
spl-token accounts
spl-token accounts TOKEN_MINT_ADDRESS

# 获取代币供应量
spl-token supply TOKEN_MINT_ADDRESS

# 获取代币详细信息
spl-token account-info TOKEN_MINT_ADDRESS
```

### 3. 多重签名支持

```sh
# 创建多重签名代币账户
spl-token create-account TOKEN_MINT_ADDRESS --multisig 2 SIGNER1 SIGNER2 SIGNER3

# 使用多重签名转移代币
spl-token transfer SOURCE_ACCOUNT 100 DESTINATION_ACCOUNT --multisig SIGNER1 SIGNER2
```

## 代币标准支持

### 1. SPL Token 2022 (最新标准)

```sh
# 创建 SPL Token 2022 代币
spl-token create-token --token-program-id TokenzQdBNbLqP5VEhdkAS6EP7P5e2bRgEg9F88

# 铸造 SPL Token 2022 代币
spl-token mint TOKEN_MINT_ADDRESS 1000 --token-program-id TokenzQdBNbLqP5VEhdkAS6EP7P5e2bRgEg9F88
```

### 2. NFT (Non-Fungible Token)

```sh
# 创建 NFT Mint
spl-token create-token --decimals 0 --name "My NFT" --symbol "NFT"

# 铸造 NFT (供应量为 1)
spl-token mint TOKEN_MINT_ADDRESS 1

# 创建 NFT 元数据账户
spl-token create-metadata TOKEN_MINT_ADDRESS --uri "https://example.com/metadata.json"
```

### 3. USDC 和其他稳定币

```sh
# USDC 代币地址 (主网)
USDC_MAINNET="EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyMgV7"

# USDC 代币地址 (测试网)
USDC_DEVNET="AxsRgNNR4qFxGCa8ijbQ5jN2nevYz6ZL5qTPtu3Xay5v"

# 检查 USDC 余额
spl-token balance $USDC_MAINNET
```

## 批量操作

### 1. 批量空投

```sh
# 从文件读取地址进行批量空投
spl-token bulk-airdrop TOKEN_MINT_ADDRESS addresses.txt 10

# 批量转移
spl-token bulk-transfer SOURCE_ACCOUNT transfers.csv
```

### 2. 批量账户管理

```sh
# 批量创建账户
spl-token batch-create-accounts TOKEN_MINT_ADDRESS addresses.txt

# 批量关闭账户
spl-token batch-close-accounts accounts.txt
```

## 安全功能

### 1. 权限管理

```sh
# 设置代币冻结权限
spl-token authorize TOKEN_MINT_ADDRESS freeze AUTHORITY_KEYPAIR

# 设置代币供应管理权限
spl-token authorize TOKEN_MINT_ADDRESS mint AUTHORITY_KEYPAIR

# 设置代币账户权限
spl-token authorize ACCOUNT_ADDRESS owner NEW_OWNER_KEYPAIR
```

### 2. 交易安全

```sh
# 设置交易超时
spl-token --timeout 60 transfer ...

# 启用交易确认
spl-token --confirm transfer ...

# 设置最大费用
spl-token --max-fee 0.000005 transfer ...
```

## 开发和测试

### 1. 测试环境设置

```sh
# 在 devnet 上创建测试代币
spl-token create-token --url devnet

# 在本地测试验证器上使用
spl-token create-token --url http://localhost:8899
```

### 2. 模拟交易

```sh
# 模拟代币转移
spl-token simulate transfer SOURCE_ACCOUNT 100 DESTINATION_ACCOUNT

# 模拟代币铸造
spl-token simulate mint TOKEN_MINT_ADDRESS 1000
```

## 故障排除

### 1. 常见错误解决

```sh
# 检查代币账户是否存在
spl-token account-info ACCOUNT_ADDRESS

# 验证代币 Mint 地址
spl-token verify TOKEN_MINT_ADDRESS

# 检查钱包余额是否足够支付费用
solana balance
```

### 2. 调试选项

```sh
# 启用详细输出
spl-token --verbose command

# 启用调试模式
spl-token --debug command

# 显示执行时间
spl-token --timing command
```

## 最佳实践

### 1. 代币创建

- **选择合适的小数位**: 大多数代币使用 6 或 9 位小数
- **设置适当的权限**: 考虑是否需要冻结、铸造等功能
- **记录代币信息**: 保存 Mint 地址和相关密钥

### 2. 代币管理

- **定期审计**: 检查代币供应量和账户状态
- **安全存储**: 妥善保管 Mint 权限密钥
- **监控活动**: 跟踪大额转账和异常活动

### 3. 开发测试

- **使用测试网**: 在主网部署前充分测试
- **模拟真实场景**: 测试各种边界情况
- **性能优化**: 考虑批量操作提高效率

## 与其他工具集成

### 1. 与 Anchor 集成

```rust
// 在 Anchor 程序中使用 SPL Token
use anchor_spl::token::{Token, TokenAccount, Mint};

#[derive(Accounts)]
pub struct TransferTokens<'info> {
    #[account(mut)]
    pub from: Account<'info, TokenAccount>,
    #[account(mut)]
    pub to: Account<'info, TokenAccount>,
    #[account(mut)]
    pub mint: Account<'info, Mint>,
    pub token_program: Program<'info, Token>,
    pub authority: Signer<'info>,
}
```

### 2. 与前端应用集成

```typescript
// 使用 @solana/spl-token 库
import { Token, TOKEN_PROGRAM_ID } from '@solana/spl-token';

const token = new Token(
  connection,
  TOKEN_MINT_ADDRESS,
  TOKEN_PROGRAM_ID,
  wallet
);

// 创建代币账户
const tokenAccount = await token.createAccount(owner);

// 转移代币
await token.transfer(
  sourceAccount,
  destinationAccount,
  authority,
  amount
);
```

## 资源链接

- [SPL Token 标准文档](https://spl.solana.com/token)
- [SPL Token 2022 文档](https://spl.solana.com/token-2022)
- [SPL Token CLI 源码](https://github.com/solana-labs/solana-program-library/tree/master/token/cli)
- [代币开发最佳实践](https://solanacookbook.com/core-concepts/tokens.html)