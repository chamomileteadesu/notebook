# Bun

## Node Package Manager(NPM)

```sh
# 查看项目包安装目录
npm root
# 查看全局包安装目录
npm root -g

# 安装所有项目依赖
npm install

# 安装指定项目依赖
npm install PACKAGE

# 安装指定项目依赖并指定源
npm install PACKAGE --registry=https://registry.npm.taobao.org

# 安装指定项目依赖
npm install -D PACKAGE

# 卸载项目依赖
npm remove PACKAGE

# 更新项目依赖
npm update PACKAGE_NAME
# 更新全局包
npm update -g PACKAGE_NAME

# 运行 package.json 中的脚本
npm run SCRIPT

# 设置镜像，以淘宝镜像为例
npm config set registry https://registry.npm.taobao.org
# 打开 npm 配置文件
npm config edit

# 查看缓存路径
npm config get cache
# 查看缓存状态
npm cache verify
# 清除所有 npm 缓存，注意，npm 通常能够自我管理缓存
npm cache clean --force

# 查看全局安装的包，且不显示依赖树
npm list -g --depth=0

# 登录 npm
npm login

# 查看依赖包元数据信息
npm view @sveltejs/kit
npm view @sveltejs/kit version
npm view @sveltejs/kit versions
npm view @sveltejs/kit homepage
npm view @sveltejs/kit liicense
```

## Bun as a Package Manager

```sh
# 安装所有项目依赖
bun i
bun install

# 安装指定项目依赖
bun add PACKAGE

# 安装项目开发依赖
bun add -d PACKAGE

# 卸载项目依赖
bun remove PACKAGE

# 运行脚本
bun run SCRIPT

# 依据 package.json 更新项目依赖
bun update

# 忽略 package.json 更新项目依赖
bun update --latest

# 更新指定项目依赖
bun update PACKAGE

# 查看过时依赖
bun outdated

# 查看缓存
bun pm cache

# 清理缓存
bun pm cache rm

# 查看全局安装的包
bun pm ls -g

# 查看全局二进制文件路径
bun pm bin -g
```

## Bun as a Runtime

```sh
# 运行 JS/TS 文件
bun run index.ts

# 监听文件变化自动重启
bun --watch run index.ts

# 热重载（保持状态）
bun --hot run index.ts
```

## Bun as a Bundler

```sh
# 打包入口文件
bun build ./src/index.ts --outdir ./dist

# 生产环境压缩
bun build ./src/index.ts --outdir ./dist --minify

# 生成 sourcemap
bun build ./src/index.ts --outdir ./dist --sourcemap

# 指定目标环境
# browser | bun | node
bun build ./src/index.ts --target browser --outdir ./dist
```

## Bun as a Test Runner

```sh
# 运行测试
# 自动匹配 *.test.{ts,js} 文件
bun test

# 运行指定测试文件
bun test ./tests/unit.test.ts

# 监听模式
bun --watch test

# 显示覆盖率
bun test --coverage
```

```ts
// example.test.ts
import { expect, test, describe } from "bun:test";

describe("math", () => {
  test("1 + 1 = 2", () => {
    expect(1 + 1).toBe(2);
  });
});
```

## bun Executor

```sh
# 临时执行包命令
# 类似 npx，但更快
bun x cowsay "Hello"

# 执行特定版本
bun x vite@latest
```

## bun init

```sh
# 初始化新项目
bun init

# 指定模板
bun create vite my-app
bun create next-app my-app
```

## 环境变量

```sh
# 自动加载 .env 文件
# 无需 dotenv 包
bun run index.ts
```

```ts
// 访问环境变量
const key = Bun.env.API_KEY;
```
