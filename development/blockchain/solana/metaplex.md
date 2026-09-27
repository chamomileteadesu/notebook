# Metaplex CLI 工具

## 概述

Metaplex 是 Solana 生态系统中最流行的 NFT 标准和工具套件。Metaplex CLI 提供了创建、管理和部署 NFT 集合的完整功能，支持最新的 Token Metadata 标准。

## 安装

```sh
# 通过 npm 安装
npm install -g @metaplex-foundation/mpl-token-metadata-cli

# 通过 Cargo 安装
cargo install metaplex-cli

# 验证安装
metaplex --version
```

## 基础概念

### 1. NFT 标准

- **Token Metadata**: Metaplex 的核心标准，为 SPL 代币添加元数据
- **Candy Machine**: 用于批量创建和分发 NFT 的程序
- **Digital Asset Standard (DAS)**: 最新的 NFT 标准，提供更多功能

### 2. 关键组件

- **Mint Account**: NFT 的唯一标识
- **Metadata Account**: 存储 NFT 的元数据信息
- **Master Edition**: 控制 NFT 的版次和铸造
- **Collection**: NFT 集合的管理

## 基础操作

### 1. 创建 NFT

```sh
# 创建单个 NFT
metaplex create-nft \
  --name "My First NFT" \
  --symbol "MFN" \
  --uri "https://example.com/metadata.json" \
  --seller-fee-basis-points 500 \
  --creators "wallet1:100" \
  --collection "collection_mint_address"

# 创建不可变 NFT
metaplex create-nft \
  --name "Immutable NFT" \
  --symbol "INFT" \
  --uri "https://example.com/metadata.json" \
  --immutable

# 创建带属性的 NFT
metaplex create-nft \
  --name "Character NFT" \
  --symbol "CHAR" \
  --uri "https://example.com/metadata.json" \
  --attributes "background:blue,eyes:green,hair:red"
```

### 2. 管理 NFT

```sh
# 更新 NFT 元数据
metaplex update-nft \
  --mint-address MINT_ADDRESS \
  --name "Updated Name" \
  --uri "https://example.com/updated-metadata.json"

# 冻结 NFT
metaplex freeze-nft --mint-address MINT_ADDRESS

# 解冻 NFT
metaplex unfreeze-nft --mint-address MINT_ADDRESS
```

### 3. 查询 NFT

```sh
# 获取 NFT 信息
metaplex get-nft --mint-address MINT_ADDRESS

# 列出钱包的 NFT
metaplex list-nfts --wallet WALLET_ADDRESS

# 按集合查询 NFT
metaplex list-nfts --collection COLLECTION_MINT
```

## Candy Machine

### 1. 创建 Candy Machine

```sh
# 创建 Candy Machine v3
metaplex create-candy-machine \
  --authority AUTHORITY_KEYPAIR \
  --collection-mint COLLECTION_MINT \
  --items-available 1000 \
  --symbol "CM" \
  --seller-fee-basis-points 500 \
  --max-gatekeeper-period 86400 \
  --go-live-date "2024-01-01T00:00:00Z"

# 创建 Candy Machine v2 (兼容性)
metaplex create-candy-machine-v2 \
  --authority AUTHORITY_KEYPAIR \
  --items-available 1000 \
  --price 0.1 \
  --symbol "CM2" \
  --seller-fee-basis-points 500
```

### 2. 配置 Candy Machine

```sh
# 添加项目到 Candy Machine
metaplex add-items \
  --candy-machine-id CANDY_MACHINE_ID \
  --items-file items.json

# 更新 Candy Machine 配置
metaplex update-candy-machine \
  --candy-machine-id CANDY_MACHINE_ID \
  --price 0.05 \
  --go-live-date "2024-01-02T00:00:00Z"

# 设置白名单
metaplex set-whitelist \
  --candy-machine-id CANDY_MACHINE_ID \
  --whitelist-merkle-root MERKLE_ROOT
```

### 3. Candy Machine 管理

```sh
# 获取 Candy Machine 信息
metaplex get-candy-machine --candy-machine-id CANDY_MACHINE_ID

# 删除 Candy Machine 项目
metaplex delete-items \
  --candy-machine-id CANDY_MACHINE_ID \
  --index 0

# 撤销 Candy Machine
metaplex revoke-candy-machine \
  --candy-machine-id CANDY_MACHINE_ID
```

## 集合管理

### 1. 创建集合

```sh
# 创建集合 NFT
metaplex create-collection \
  --name "My Collection" \
  --symbol "MYC" \
  --uri "https://example.com/collection-metadata.json" \
  --seller-fee-basis-points 500 \
  --creators "wallet1:100"

# 创建可变集合
metaplex create-collection \
  --name "Mutable Collection" \
  --symbol "MUTC" \
  --uri "https://example.com/collection-metadata.json" \
  --mutable
```

### 2. 管理集合

```sh
# 添加 NFT 到集合
metaplex add-to-collection \
  --nft-mint NFT_MINT_ADDRESS \
  --collection-mint COLLECTION_MINT_ADDRESS

# 从集合中移除 NFT
metaplex remove-from-collection \
  --nft-mint NFT_MINT_ADDRESS \
  --collection-mint COLLECTION_MINT_ADDRESS

# 更新集合信息
metaplex update-collection \
  --collection-mint COLLECTION_MINT_ADDRESS \
  --name "Updated Collection Name"
```

## 批量操作

### 1. 批量创建 NFT

```sh
# 从配置文件批量创建
metaplex batch-create-nfts \
  --config-file nfts-config.json \
  --output-dir ./nfts-output/

# 批量更新 NFT
metaplex batch-update-nfts \
  --nfts-file nfts-list.json \
  --update-data update-data.json
```

### 2. 批量管理

```sh
# 批量添加到集合
metaplex batch-add-to-collection \
  --nfts-file nfts-list.json \
  --collection-mint COLLECTION_MINT

# 批量设置属性
metaplex batch-set-attributes \
  --nfts-file nfts-list.json \
  --attributes-file attributes.json
```

## 高级功能

### 1. 版次管理

```sh
# 创建版次 NFT
metaplex create-edition \
  --master-mint MASTER_MINT_ADDRESS \
  --edition-number 1 \
  --edition-mint NEW_EDITION_MINT

# 获取版次信息
metaplex get-edition --edition-mint EDITION_MINT_ADDRESS

# 列出所有版次
metaplex list-editions --master-mint MASTER_MINT_ADDRESS
```

### 2. 门禁控制

```sh
# 设置时间门禁
metaplex set-time-gate \
  --candy-machine-id CANDY_MACHINE_ID \
  --go-live-date "2024-01-01T00:00:00Z"

# 设置代币门禁
metaplex set-token-gate \
  --candy-machine-id CANDY_MACHINE_ID \
  --required-token TOKEN_MINT_ADDRESS \
  --required-amount 1

# 设置白名单门禁
metaplex set-whitelist-gate \
  --candy-machine-id CANDY_MACHINE_ID \
  --whitelist-merkle-root MERKLE_ROOT
```

### 3. 自定义程序

```sh
# 部署自定义元数据程序
metaplex deploy-program \
  --program-id CUSTOM_PROGRAM_ID \
  --source-code ./custom-program/

# 注册自定义元数据
metaplex register-custom-metadata \
  --mint-address MINT_ADDRESS \
  --custom-program-id CUSTOM_PROGRAM_ID \
  --custom-data "custom_data.json"
```

## 开发和测试

### 1. 本地开发

```sh
# 在本地网络上测试
metaplex create-nft \
  --name "Test NFT" \
  --symbol "TEST" \
  --uri "https://example.com/test-metadata.json" \
  --url http://localhost:8899

# 在 devnet 上测试
metaplex create-nft \
  --name "Devnet NFT" \
  --symbol "DEV" \
  --uri "https://example.com/dev-metadata.json" \
  --url https://api.devnet.solana.com
```

### 2. 模拟操作

```sh
# 模拟 NFT 创建
metaplex simulate-create-nft \
  --name "Simulated NFT" \
  --symbol "SIM" \
  --uri "https://example.com/sim-metadata.json"

# 模拟 Candy Machine 铸造
metaplex simulate-mint \
  --candy-machine-id CANDY_MACHINE_ID \
  --wallet WALLET_ADDRESS
```

## 故障排除

### 1. 常见问题

```sh
# 检查网络连接
metaplex ping --url https://api.mainnet-beta.solana.com

# 验证配置文件
metaplex validate-config --config-file config.json

# 检查余额
solana balance --keypair wallet.json
```

### 2. 调试选项

```sh
# 启用详细输出
metaplex --verbose create-nft ...

# 启用调试模式
metaplex --debug create-nft ...

# 显示执行时间
metaplex --timing create-nft ...
```

## 最佳实践

### 1. NFT 创建

- **元数据标准化**: 使用标准的 JSON Schema
- **图像优化**: 使用适当的文件格式和大小
- **属性结构化**: 使用一致的属性命名和值格式

### 2. Candy Machine

- **安全配置**: 设置适当的门禁和限制
- **测试充分**: 在主网前充分测试
- **监控活动**: 跟踪铸造进度和异常

### 3. 集合管理

- **清晰命名**: 使用有意义的集合名称和符号
- **一致主题**: 保持集合内 NFT 的主题一致性
- **权限控制**: 合理设置集合管理权限

## 与其他工具集成

### 1. 与 Anchor 集成

```rust
// 在 Anchor 程序中使用 Metaplex
use mpl_token_metadata::state::Metadata;

#[derive(Accounts)]
pub struct CreateNft<'info> {
    #[account(mut)]
    pub payer: Signer<'info>,
    #[account(init, payer = payer, space = 1000)]
    pub metadata: Account<'info, Metadata>,
    pub system_program: Program<'info, System>,
    pub token_metadata_program: Program<'info, TokenMetadata>,
}
```

### 2. 与前端应用集成

```typescript
// 使用 @metaplex-foundation/js
import { Metaplex } from '@metaplex-foundation/js';

const mx = Metaplex.make(connection);
const nft = await mx.nfts().findByMint({ mintAddress });

// 创建 NFT
const { nft: newNft } = await mx.nfts().create({
  uri: 'https://example.com/metadata.json',
  name: 'My NFT',
  sellerFeeBasisPoints: 500,
});
```

## 资源链接

- [Metaplex 官方文档](https://docs.metaplex.com/)
- [Token Metadata 标准](https://docs.metaplex.com/programs/token-metadata/overview)
- [Candy Machine 文档](https://docs.metaplex.com/programs/candy-machine/overview)
- [Metaplex CLI 源码](https://github.com/metaplex-foundation/metaplex-cli)
- [NFT 开发最佳实践](https://solanacookbook.com/nfts/overview-nfts.html)