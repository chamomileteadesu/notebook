# Node Version Manager(NVM)

- [Node Version Manager(NVM)](#node-version-managernvm)
  - [概述](#概述)
  - [安装](#安装)
    - [Linux/macOS](#linuxmacos)
    - [Windows](#windows)
  - [基本用法](#基本用法)
    - [查看可用的 Node.js 版本](#查看可用的-nodejs-版本)
    - [安装 Node.js 版本](#安装-nodejs-版本)
    - [切换 Node.js 版本](#切换-nodejs-版本)
    - [设置默认版本](#设置默认版本)
  - [高级用法](#高级用法)
    - [在项目中使用特定版本](#在项目中使用特定版本)
    - [管理已安装的版本](#管理已安装的版本)
    - [npm 管理](#npm-管理)
  - [常用命令速查](#常用命令速查)
  - [故障排除](#故障排除)
    - [常见问题](#常见问题)
    - [环境变量](#环境变量)
  - [最佳实践](#最佳实践)
  - [与其他工具的集成](#与其他工具的集成)
    - [与 IDE 集成](#与-ide-集成)
    - [与 CI/CD 集成](#与-cicd-集成)
  - [参考资源](#参考资源)

## 概述

NVM (Node Version Manager) 是一个用于管理多个 Node.js 版本的命令行工具。它允许开发者在同一台机器上安装、切换和管理不同版本的 Node.js，这对于需要在不同项目中使用不同 Node.js 版本的开发者来说非常有用。

## 安装

### Linux/macOS

```bash
# 使用 curl 安装
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash

# 或使用 wget 安装
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
```

安装完成后，重启终端或运行以下命令：

```bash
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # 加载 nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # 加载 bash 补全
```

### Windows

Windows 用户可以使用 [nvm-windows](https://github.com/coreybutler/nvm-windows)：

```bash
# 下载并安装 nvm-windows
# 或使用 chocolatey
choco install nvm

# 或使用 scoop
scoop install nvm
```

## 基本用法

### 查看可用的 Node.js 版本

```bash
# 列出所有远程可用版本
nvm list remote

# 列出特定版本（如 LTS 版本）
nvm list remote --lts

# 列出已安装的版本
nvm list

# 列出已安装的版本（包括别名）
nvm list --all
```

### 安装 Node.js 版本

```bash
# 安装最新版本
nvm install node

# 安装特定版本
nvm install 18.17.0

# 安装最新的 LTS 版本
nvm install --lts

# 安装特定的 LTS 版本
nvm install lts/fermium  # Node.js 14.x
nvm install lts/gallium   # Node.js 16.x
nvm install lts/hydrogen  # Node.js 18.x
nvm install lts/iron      # Node.js 20.x
```

### 切换 Node.js 版本

```bash
# 使用特定版本
nvm use 18.17.0

# 使用系统默认版本
nvm use system

# 使用最新版本
nvm use node

# 使用 LTS 版本
nvm use --lts

# 设置默认版本（重启终端后自动使用）
nvm alias default 18.17.0

# 查看当前使用的版本
nvm current
```

### 设置默认版本

```bash
# 设置默认版本
nvm alias default 18.17.0

# 查看所有别名
nvm alias

# 删除别名
nvm unalias default
```

## 高级用法

### 在项目中使用特定版本

在项目根目录创建 `.nvmrc` 文件：

```bash
# 创建 .nvmrc 文件
echo "18.17.0" > .nvmrc

# 或指定 LTS 版本
echo "lts/hydrogen" > .nvmrc

# 或使用最新版本
echo "node" > .nvmrc
```

然后在项目目录中运行：

```bash
# 使用 .nvmrc 中指定的版本
nvm use

# 安装 .nvmrc 中指定的版本（如果未安装）
nvm install
```

### 管理已安装的版本

```bash
# 卸载特定版本
nvm uninstall 16.20.0

# 查看某个版本的详细信息
nvm ls-remote --lts | grep "18\."

# 检查版本是否已安装
nvm ls | grep "18\."
```

### npm 管理

```bash
# 查看当前 npm 版本
npm --version

# 更新 npm 到最新版本
npm install -g npm@latest

# 在不同 Node.js 版本间共享 npm 包
nvm use 18.17.0
npm install -g <package-name>

nvm use 20.12.0
# 包仍然可用，因为是全局安装的
```

## 常用命令速查

| 命令 | 描述 |
|------|------|
| `nvm install <version>` | 安装指定版本的 Node.js |
| `nvm use <version>` | 切换到指定版本 |
| `nvm ls` | 列出已安装的版本 |
| `nvm ls-remote` | 列出远程可用版本 |
| `nvm current` | 显示当前使用的版本 |
| `nvm alias default <version>` | 设置默认版本 |
| `nvm uninstall <version>` | 卸载指定版本 |
| `nvm run <version> -- <args>` | 使用指定版本运行脚本 |

## 故障排除

### 常见问题

1. **nvm 命令未找到**
   ```bash
   # 检查 nvm 是否正确安装
   command -v nvm
   
   # 重新加载 nvm
   source ~/.bashrc  # 或 ~/.zshrc
   ```

2. **版本切换失败**
   ```bash
   # 检查版本是否已安装
   nvm list
   
   # 重新安装版本
   nvm install 18.17.0
   ```

3. **npm 全局包路径问题**
   ```bash
   # 查看当前 npm 全局路径
   npm config get prefix
   
   # 为每个 Node.js 版本设置独立的全局路径
   nvm use 18.17.0
   npm config set prefix ~/.nvm/versions/node/v18.17.0
   ```

### 环境变量

```bash
# 查看 nvm 相关环境变量
echo $NVM_DIR
echo $NVM_BIN
echo $NVM_INC

# 手动设置（通常不需要）
export NVM_DIR="$HOME/.nvm"
source "$NVM_DIR/nvm.sh"
```

## 最佳实践

1. **项目级别的版本管理**
   - 在每个项目中使用 `.nvmrc` 文件
   - 在 `package.json` 中指定 `engines.node` 字段

2. **版本选择策略**
   - 新项目使用最新的 LTS 版本
   - 现有项目保持与生产环境一致的版本
   - 测试项目可以使用最新版本

3. **定期更新**
   ```bash
   # 更新 nvm 本身
   nvm install node --reinstall-packages-from=node
   
   # 清理旧版本
   nvm uninstall 14.21.3
   ```

## 与其他工具的集成

### 与 IDE 集成

大多数现代 IDE（如 VS Code、WebStorm）都能自动检测 `.nvmrc` 文件并使用相应的 Node.js 版本。

### 与 CI/CD 集成

在 GitHub Actions、GitLab CI 等中使用：

```yaml
# GitHub Actions 示例
- uses: actions/setup-node@v3
  with:
    node-version: '18.x'
    cache: 'npm'
```

## 参考资源

- [NVM 官方仓库](https://github.com/nvm-sh/nvm)
- [Node.js 官方文档](https://nodejs.org/en/docs/)
- [Node.js 版本发布日程](https://nodejs.org/en/about/releases/)
