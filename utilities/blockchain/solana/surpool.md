# Surfpool

## 概述

Surfpool 是 Solana 开发工具链中的革命性工具，作为 solana-test-validator 的强大替代品。它专为提升 Solana 开发者的体验而设计，提供了更快的启动速度、更强大的功能和更好的开发效率。

## 核心特性

### 1. 主网数据即时获取 (Mainnet Forking)

Surfpool 的核心优势是能够从主网即时获取账户数据，让你在本地环境中测试真实的主网状态。

```sh
# 启动 Surfpool
surfpool start

# 启动并指定端口
surfpool start --port 8899

# 启动并指定 RPC 端点
surfpool start --rpc-url https://api.mainnet-beta.solana.com
```

### 2. 基础功能

```sh
# 启动 Surfpool
surfpool start

# 停止 Surfpool
surfpool stop

# 重启 Surfpool
surfpool restart

# 查看 Surfpool 状态
surfpool status

# 查看版本信息
surfpool --version
```

### 3. 配置选项

```sh
# 使用配置文件启动
surfpool start --config Surfpool.toml

# 指定槽位时间 (默认 400ms)
surfpool start --slot-time 500

# 指定纪元持续时间 (默认 432,000)
surfpool start --epoch-duration 432000

# 设置 RPC 超时
surfpool start --rpc-timeout 30
```

## 与 Anchor 集成

### 1. 基础集成

```toml
# Anchor.toml 配置
[provider]
cluster = "http://localhost:8899"
wallet = "~/.config/solana/id.json"

[scripts]
test = "anchor test --skip-local-validator"
```

### 2. 高级配置

```toml
# Surfpool.toml 配置文件
[general]
slot_time = 400
epoch_duration = 432000
rpc_timeout = 30

[rpc]
url = "https://api.mainnet-beta.solana.com"
port = 8899

[cheatcodes]
enabled = true
max_accounts = 1000

[debug]
verbose = true
log_level = "info"
```

## 开发工作流程

### 1. 本地开发环境设置

```sh
# 1. 启动 Surfpool
surfpool start

# 2. 验证 Surfpool 运行状态
surfpool status

# 3. 运行 Anchor 测试
anchor test --skip-local-validator

# 4. 停止 Surfpool
surfpool stop
```

### 2. 主网分叉测试

```sh
# 启动主网分叉模式
surfpool start --fork-mainnet

# 指定分叉的槽位
surfpool start --fork-mainnet --slot 300000000

# 使用自定义 RPC 端点
surfpool start --fork-mainnet --rpc-url https://your-rpc-endpoint.com
```

### 3. 状态操作 (Cheatcodes)

Surfpool 提供了强大的状态操作功能，用于测试和调试：

```sh
# 设置账户余额
surfpool cheatcode set-balance ACCOUNT_ADDRESS 10

# 设置账户数据
surfpool cheatcode set-data ACCOUNT_ADDRESS "0x1234..."

# 模拟交易失败
surfpool cheatcode fail-transaction TX_SIGNATURE

# 快进时间
surfpool cheatcode fast-forward 1000

# 重置状态
surfpool cheatcode reset-state
```

## WebSocket RPC 支持

Surfpool 支持实时的 WebSocket 订阅，适用于需要实时状态更新的应用：

```sh
# 启用 WebSocket 支持
surfpool start --websocket

# 指定 WebSocket 端口
surfpool start --websocket --ws-port 8900

# 测试 WebSocket 连接
surfpool test-websocket
```

## 基础设施即代码 (IaC)

### 1. 基础 IaC 配置

```toml
# deployment.txtx - Surfpool IaC 配置
name: "My Solana Deployment"
version: "1.0.0"

networks:
  local:
    rpc_url: "http://localhost:8899"
    chain_id: "localnet"

contracts:
  my_program:
    path: "./target/deploy/my_program.so"
    id: "MyProgramId"
    authority: "wallet.json"

accounts:
  test_account:
    balance: 10
    data: "0x00"
```

### 2. 部署到不同网络

```sh
# 部署到本地网络
surfpool deploy --network local --config deployment.txtx

# 部署到 devnet
surfpool deploy --network devnet --config deployment.txtx

# 部署到 mainnet (谨慎使用!)
surfpool deploy --network mainnet --config deployment.txtx
```

## 性能优化

### 1. 启动速度优化

```sh
# 使用内存模式 (更快但重启后数据丢失)
surfpool start --memory-mode

# 预加载常用账户
surfpool start --preload-accounts ACCOUNT1,ACCOUNT2,ACCOUNT3

# 启用缓存
surfpool start --cache-enabled
```

### 2. 内存管理

```sh
# 限制内存使用
surfpool start --memory-limit 2G

# 启用垃圾回收
surfpool start --gc-enabled

# 设置最大连接数
surfpool start --max-connections 100
```

## 故障排除

### 1. 常见问题解决

```sh
# 检查端口占用
surfpool check-port 8899

# 清理缓存
surfpool clean --cache

# 重置状态
surfpool reset

# 查看日志
surfpool logs --follow

# 调试模式启动
surfpool start --debug
```

### 2. 网络问题排查

```sh
# 测试 RPC 连接
surfpool test-rpc --url https://api.mainnet-beta.solana.com

# 检查网络延迟
surfpool ping --url https://api.devnet.solana.com

# 验证区块哈希
surfpool verify-blockhash --hash BLOCKHASH
```

## 与 solana-test-validator 对比

| 特性 | solana-test-validator | Surfpool |
| --- | --- | --- |
| 启动速度 | 较慢 | 快速 |
| 主网数据支持 | 不支持 | 支持即时获取 |
| 状态操作 | 有限 | 强大的 Cheatcodes |
| WebSocket 支持 | 基础 | 完整支持 |
| 配置灵活性 | 有限 | 高度可配置 |
| IaC 支持 | 不支持 | 完整支持 |
| 内存使用 | 较高 | 优化 |
| 开发体验 | 基础 | 优秀 |

## 最佳实践

### 1. 开发环境配置

```sh
# 1. 创建配置文件
cat > Surfpool.toml << EOF
[general]
slot_time = 400
epoch_duration = 432000

[rpc]
url = "https://api.devnet.solana.com"
port = 8899
EOF

# 2. 启动 Surfpool
surfpool start --config Surfpool.toml

# 3. 运行测试
anchor test --skip-local-validator
```

### 2. CI/CD 集成

```yaml
# .github/workflows/test.yml
name: Test with Surfpool
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Install Surfpool
        run: curl -sL https://run.surfpool.run | bash
      - name: Start Surfpool
        run: surfpool start
      - name: Run tests
        run: anchor test --skip-local-validator
      - name: Stop Surfpool
        run: surfpool stop
```

### 3. 团队协作

```sh
# 共享配置
git add Surfpool.toml
git add deployment.txtx

# 文档化使用方法
echo "使用 Surfpool 进行本地开发:
1. surfpool start
2. anchor test --skip-local-validator
3. surfpool stop" > DEVELOPMENT.md
```

## 高级功能

### 1. 自定义 RPC 方法

```sh
# 注册自定义 RPC 方法
surfpool rpc register --method custom_method --handler handler.js

# 调用自定义方法
surfpool rpc call --method custom_method --params '{"key": "value"}'
```

### 2. 模拟网络条件

```sh
# 模拟高延迟网络
surfpool start --latency 500ms

# 模拟网络分区
surfpool network-partition --nodes node1,node2

# 模拟节点故障
surfpool simulate-failure --node node1 --duration 30s
```

### 3. 性能监控

```sh
# 启用性能监控
surfpool start --monitoring

# 查看性能指标
surfpool metrics

# 导出性能数据
surfpool export-metrics --format json --output metrics.json
```

## 资源和文档

- [官方文档](https://docs.surfpool.run/)
- [GitHub 仓库](https://github.com/txtx/surfpool)
- [API 参考](https://docs.surfpool.run/api)
- [社区支持](https://discord.gg/surfpool)
- [视频教程](https://docs.surfpool.run/tutorials)
