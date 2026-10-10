# Anchor

## 概述

Anchor 是 Solana 生态系统中最广泛采用的开发框架，由 Armani Ferrante 和 Coral 团队创建和维护。它为使用 Rust 构建 Solana 程序（智能合约）提供了简化的开发体验，通过提供类型安全的代码生成、自动化的测试框架和简化的部署流程来降低开发门槛。

## 最新版本特性 (v0.31.0+)

### 核心改进
- **性能优化**: 显著提升编译速度和运行时性能
- **类型安全增强**: 更严格的类型检查和更好的错误提示
- **代码生成优化**: 减少生成代码的冗余，提高可读性
- **兼容性**: 支持最新的 Solana 版本 (2.1.0+)

### 新增功能
- **事件发射改进**: 更高效的事件处理机制
- **跨程序调用优化**: 简化 CPI (Cross-Program Invocation) 的使用
- **访问控制增强**: 更灵活的权限管理
- **宏系统改进**: 更强大的代码生成能力

## 基础使用

### 项目初始化

```sh
# 创建一个新的 anchor 项目
anchor init my-project

# 使用特定模板创建项目
anchor init my-project --template <template-name>

# 初始化现有目录为 anchor 项目
cd existing-project && anchor init .
```

### 项目结构

```
my-project/
├── Anchor.toml          # Anchor 配置文件
├── Cargo.toml          # Rust 项目配置
├── programs/           # 程序源码
│   └── my-project/
│       ├── Cargo.toml
│       └── src/lib.rs
├── tests/              # TypeScript 测试
│   └── my-project.ts
└── app/               # 前端应用 (可选)
```

### 构建和部署

```sh
# 构建项目
anchor build

# 构建并部署到 devnet
anchor deploy --provider.cluster devnet

# 构建并部署到 mainnet
anchor deploy --provider.cluster mainnet

# 验证部署的程序 (v0.31.0+ 新功能)
anchor verify <program-id>
```

## 开发工作流程

### 1. 定义程序逻辑

在 `programs/my-project/src/lib.rs` 中定义程序：

```rust
use anchor_lang::prelude::*;

declare_id!("YourProgramIDHere");

#[program]
pub mod my_project {
    use super::*;

    pub fn initialize(ctx: Context<Initialize>, data: u64) -> Result<()> {
        ctx.accounts.new_account.data = data;
        Ok(())
    }

    pub fn update(ctx: Context<Update>, data: u64) -> Result<()> {
        ctx.accounts.account.data = data;
        Ok(())
    }
}

#[derive(Accounts)]
pub struct Initialize<'info> {
    #[account(init, payer = user, space = 8 + 8)]
    pub new_account: Account<'info, MyAccount>,
    #[account(mut)]
    pub user: Signer<'info>,
    pub system_program: Program<'info, System>,
}

#[derive(Accounts)]
pub struct Update<'info> {
    #[account(mut)]
    pub account: Account<'info, MyAccount>,
}

#[account]
pub struct MyAccount {
    pub data: u64,
}
```

### 2. 编写测试

在 `tests/my-project.ts` 中编写 TypeScript 测试：

```typescript
import * as anchor from '@project-serum/anchor';
import { Program } from '@project-serum/anchor';
import { MyProject } from '../target/types/my_project';

describe('my-project', () => {
  const provider = anchor.AnchorProvider.env();
  anchor.setProvider(provider);

  const program = anchor.workspace.MyProject as Program<MyProject>;

  it('Is initialized!', async () => {
    const myAccount = anchor.web3.Keypair.generate();

    await program.rpc.initialize(new anchor.BN(42), {
      accounts: {
        newAccount: myAccount.publicKey,
        user: provider.wallet.publicKey,
        systemProgram: anchor.web3.SystemProgram.programId,
      },
      signers: [myAccount],
    });

    const account = await program.account.myAccount.fetch(myAccount.publicKey);
    console.log('Data is: ', account.data.toString());
  });
});
```

### 3. 测试和本地开发

```sh
# 使用 solana-test-validator 运行测试
anchor test

# 使用 surfpool 运行测试 (推荐)
anchor test --skip-local-validator

# 在测试中指定 surfpool 端点
anchor test --skip-local-validator --provider.cluster http://localhost:8899

# 运行特定测试
anchor test -- --grep "specific test name"
```

## 高级功能

### 事件发射

```rust
#[program]
pub mod my_project {
    use super::*;

    pub fn emit_event(ctx: Context<EmitEvent>) -> Result<()> {
        emit!(MyEvent {
            message: "Hello Anchor!".to_string(),
            timestamp: Clock::get()?.unix_timestamp,
        });
        Ok(())
    }
}

#[event]
pub struct MyEvent {
    #[index]
    pub message: String,
    pub timestamp: i64,
}
```

### 访问控制

```rust
#[derive(Accounts)]
pub struct AdminOnly<'info> {
    #[account(constraint = authority.key() == ADMIN_PUBKEY)]
    pub authority: Signer<'info>,
    // ... 其他账户
}

const ADMIN_PUBKEY: Pubkey = pubkey!("AdminPublicKeyHere");
```

### 跨程序调用 (CPI)

```rust
pub fn cpi_call(ctx: Context<CpiCall>, amount: u64) -> Result<()> {
    let cpi_program = ctx.accounts.token_program.to_account_info();
    let cpi_accounts = Transfer {
        from: ctx.accounts.from.to_account_info(),
        to: ctx.accounts.to.to_account_info(),
        authority: ctx.accounts.authority.to_account_info(),
    };
    let cpi_ctx = CpiContext::new(cpi_program, cpi_accounts);
    anchor_spl::token::transfer(cpi_ctx, amount)
}
```

## 最佳实践

### 1. 安全性

- **输入验证**: 始终验证用户输入
- **权限检查**: 使用 `#[account(signer)]` 和 `#[account(constraint = ...)]`
- **溢出保护**: 使用 `anchor_lang::solana_program::checked_math`
- **重入保护**: 避免在状态更新前调用外部程序

### 2. 性能优化

- **最小化账户空间**: 只分配必要的空间
- **批量操作**: 减少程序调用次数
- **缓存常用数据**: 避免重复计算

### 3. 测试策略

- **单元测试**: 测试单个函数逻辑
- **集成测试**: 测试完整的程序交互
- **压力测试**: 测试高负载场景

## 部署和验证

### 部署到不同网络

```sh
# 部署到 devnet
anchor deploy --provider.cluster devnet

# 部署到 testnet
anchor deploy --provider.cluster testnet

# 部署到 mainnet (需要谨慎!)
anchor deploy --provider.cluster mainnet-beta
```

### 程序验证

```sh
# 验证部署的程序源码 (v0.31.0+)
anchor verify <program-id> --source <source-directory>

# 验证特定版本
anchor verify <program-id> --version 0.31.0
```

## 常见问题解决

### 编译错误

```sh
# 清理并重新构建
anchor clean
anchor build

# 检查 Rust 版本兼容性
rustc --version
cargo --version
```

### 测试失败

```sh
# 重置测试环境
solana-test-validator --reset

# 使用 surfpool 替代
surfpool start
```

### 部署问题

```sh
# 检查钱包余额
solana balance

# 请求空投 (devnet)
solana airdrop 2
```

## 工具集成

### 与 Surfpool 集成

```toml
# Anchor.toml
[provider]
cluster = "http://localhost:8899"
wallet = "~/.config/solana/id.json"

[scripts]
test = "anchor test --skip-local-validator"
```

### 与前端框架集成

```typescript
// React 示例
import { useAnchorWallet } from '@solana/wallet-adapter-react';
import { Program, AnchorProvider, web3 } from '@project-serum/anchor';

const MyComponent = () => {
  const wallet = useAnchorWallet();
  const connection = new web3.Connection(web3.clusterApiUrl('devnet'));
  const provider = new AnchorProvider(connection, wallet, {});
  const program = new Program(idl, programId, provider);

  const handleInitialize = async () => {
    const myAccount = web3.Keypair.generate();
    await program.rpc.initialize(new anchor.BN(42), {
      accounts: {
        newAccount: myAccount.publicKey,
        user: wallet.publicKey,
        systemProgram: web3.SystemProgram.programId,
      },
      signers: [myAccount],
    });
  };

  return <button onClick={handleInitialize}>Initialize</button>;
};
```

## 资源和文档

- [官方文档](https://book.anchor-lang.com/)
- [GitHub 仓库](https://github.com/coral-xyz/anchor)
- [API 参考](https://docs.rs/anchor-lang/)
- [社区论坛](https://discord.gg/anchor)
