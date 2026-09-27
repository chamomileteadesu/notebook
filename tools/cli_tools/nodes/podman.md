# Podman

## 系统管理

```sh
# 查看版本
podman version
# 查看信息
podman info
```

## 镜像搜索与拉取

```sh
# 搜索镜像
podman search name
# 过滤stars小于3000的镜像
podman search name --filter=stars=3000
# 拉取镜像
podman pull name:version
```

## 本地镜像管理

```sh
# 查看本地镜像
podman images
-a # 显示所有镜像
podman images
# 只显示镜像 id
podman images -q

# 删除镜像
podman image rm [name:version|id]
# 删除镜像
podman rmi [name:version|id]
# 强制删除镜像
podman image rm -f [name:version|id]
```

## 镜像保存与加载及分享

```sh
# 镜像另存为本地文件
podman save nginx:latest >> nginx.tar
#　or
podman save nginx:latest -o nginx.tar

# 从本地文件加载镜像
podman load -i nginx.tar

# 将一个容器打包为镜像
podman commit -m 'message' CONTAINER [镜像名[:标签]]

# 登陆
podman login
# 迎合社区规范，为镜像添加标签
podman tag xxx:v1.0 dockerhub_username/xxx:v1.0
# 推送镜像
podman push dockerhub_username/xxx:v1.0

# 将一个 Podman 容器的文件系统导出为一个 .tar 归档文件
podman export [OPTIONS] CONTAINER >> xxx.tar
# or
podman export [OPTIONS] CONTAINER -o xxx.tar

# 将一个 .tar 归档文件导入为 Podman 镜像
# xxx.tar 可以存在于网络上
podman import [OPTIONS] xxx.tar IMAGE_NAME[:tag]
```

## 创建或删除容器

```sh
# 创建容器
podman create name
# 删除一个容器
podman rm [name|id]
# 强制删除一个容器
podman rm -f [name|id]
```

## 容器运行

```sh
podman run \
-d \                          # 让容器在后台运行
--name mysql \                # 为容器起名
-p 3306:3306 \                # 端口映射
-e TZ=Asia/Shanghai \         # 设置环境变量
--network mynet \             # 指定一个 podman 网络，默认为 docker0
--ip=172.16.0.8 \             # 指定一个 ip 地址
--restart=unless-stopped \    # 设置容器重启策略
mysql:5.7
```

## 容器状态管理

```sh
# 查看活动容器
podman ps
# 查看所有容器
podman ps -a
# 查看容器状态
podman status [name|id]
# 查看一个容器
podman inspect [name|id]
# 启动容器
podman start [name|id]
# 重启容器
podman restart [name|id]
# 暂停容器
podman stop [name|id]
# 杀死容器
podman kill [name|id]
```

## 容器执行

```sh
# 以交互方式执行容器内的二进制程序
podman exec -it [name|id] PROGRAM
```

## cp

```sh
podman cp <本地目录> <容器:容器内的目录>
podman cp <容器:容器内的目录> <本地目录>
```

## logs

```sh
# 查看日志
podman logs [name|id]
# 实时显示日志
podman logs -f [name|id]
```

## 数据卷

```sh
# 创建一个匿名数据卷
podman volume create

# 创建一个数据卷
podman volume create volume_name

# 查看所有数据卷
podman volume ls

# 删除指定数据卷
podman volume rm

# 查看某个数据卷
podman volume inspect

# 清除匿名数据卷
podman volume prune

# 导出数据卷
podman volume export VOLUME_NAME --output OUTPUT_FILE_NAME.TAR

# 卷映射
# 若数据卷/本地目录不存在将自动创建
podman run -v 数据卷:容器内挂载点
# 目录挂载
podman run -v 本地目录:容器内目录
```

## podman 网络

```sh
# 创建一个网络 mynet
podman network create mynet
# 查看某个网络详情
podman network inspect mynet
# 查看所有网络
podman network ls
# 删除一个网络
podman network rm mynet
# 清除未使用网络
podman network prune
# 使容器 nginx 加入 mynet
podman network connect mynet nginx
# 使容器 nginx 离开 mynet
podman network disconnect mynet nginx
```

## podman-compose.yaml

### podman-compose.yaml 文件的书写

```yaml
# podman compose 版本
version: "3.9"

# 应用名
name: myapp

# 服务清单
services:
    mysql:
        container_name: mysql
        image: mysql:8.0
        ports:
            - "3306:3306"
        environment:
            TZ: Asia/Shanghai
            MYSQL_ROOT_PASSWORD: 123456
        volumes:
            - "mysql-data:/var/lib/mysql"
            - "/app/myconf:/etc/mysql/conf.d"
        networks:
            - mynet
        restart: always
    nginx:
        ...
        depends_on:
            - mysql
# 数据卷声明
volumes:
    mysql-data:
        driver: local
# 网络声明
networks:
    mynet:
        driver: bridge
```

### 使用 podman-compose.yaml

```sh
# 指定使用 compose.yaml，在后台上线一个应用
podman-compose -f compose.yaml up -d
# 下线一个应用
podman-compose -f compose.yaml down
# 列出所有启动的容器
podman-compoer -f compose.yaml ps
# 查看运行的进程
podman-compose -f compose.yaml top
# 查看指定容器的日志
podman-compose -f compose.yaml logs [name|id]
# 启动容器
podman-compose -f compose.yaml start [name|id]
# 停止容器
podman-compose -f compose.yaml stop [name|id]
# 重启容器
podman-compose -f compose.yaml restart [name|id]
# 容器执行
podman-compose -f compose.yaml exec -it [name|id] bash
```

## 镜像制作

> 场景：创建一个 Rust Web Server，访问（GET）PORT 端口（这个端口号会以环境变量的形式提供，为了演示，我们打算传入 10086 作为端口）返回 "Hello, World!"。

### 编写 Rust Web Server 代码

创建 Rust 项目：`cargo new hello-rust-server`
进入项目目录：`cd hello-rust-server`

Cargo.toml

```toml
[package]
name = "hello-rust-server"
version = "0.1.0"
edition = "2024"

[dependencies]
axum = "0.7"
tokio = { version = "1", features = ["full"] }
```

src/main.rs

```rust
use axum::{routing::get, Router};
use std::env;
use std::net::SocketAddr;

async fn hello_world_handler() -> &'static str {
    "Hello, World!"
}

#[tokio::main]
async fn main() {
    let app = Router::new().route("/", get(hello_world_handler));
    let port = env::var("PORT")
        .ok()
        .and_then(|s| s.parse().ok())
        .unwrap_or(3000);
    let addr = SocketAddr::from(([0, 0, 0, 0], port));
    println!("🚀 Server listening on {}", addr);
    let listener = tokio::net::TcpListener::bind(addr).await.unwrap();
    axum::serve(listener, app).await.unwrap();
}
```

实际开发中，你应该在本地先测试一下你的代码

```sh
PORT=10086 cargo run
```

### 编写 Dockerfile

一般在 Rust 项目根目录中创建 `Dockerfile`，也可以叫 `Containerfile`

```dockerfile
# 阶段一：构建
# 声明基础镜像
# 我们给这个阶段起个名字叫 "builder"，方便后面引用。
FROM docker.io/library/rust:1-bullseye AS builder

# optional: 自定义标签
LABEL Auther=mizu

# 设置容器内的工作目录
# 后续命令都会在这个目录下进行
WORKDIR /usr/src/app

# 拷贝 Cargo 项目配置文件到容器内工作目录
COPY Cargo.toml Cargo.lock ./

# 复制源代码
COPY src ./src

# 容器内安装 musl 编译目标
RUN rustup target add x86_64-unknown-linux-musl

# 使用 RUN 在容器内执行命令
# 构建我们的应用
# --locked 确保使用 Cargo.lock 中指定的依赖版本，保证构建的可复现性。
# --target x86_64-unknown-linux-musl 会进行静态链接，
# 这样我们的二进制文件就不依赖于系统 libc ，可以运行在更精简的环境中
RUN cargo build --release --locked --target x86_64-unknown-linux-musl

# 阶段二：运行
# 我们选择一个超级小的基础镜像
# scratch 是一个完全空白的镜像，
# 里面什么都没有，提供了极致的精简和安全
FROM scratch AS runner

# 从 "builder" 阶段复制编译好的二进制文件到新镜像的 /bin/ 目录下
COPY --from=builder /usr/src/app/target/x86_64-unknown-linux-musl/release/hello-rust-server /bin/hello-rust-server

# 暴露端口
# 这主要用于文档目的，告诉使用者这个容器内部使用哪个端口
# 没有任何实际作用
EXPOSE 6666

# 设置容器启动时要执行的命令
CMD ["/bin/hello-rust-server"]
```

### 创建 .dockerignore

为了防止不必要的文件（比如 target 目录、.git 目录）被发送到 Docker/Podman 的构建守护进程中，我们创建一个 `.dockerignore` 文件。这能加快构建速度。

在项目根目录创建 `.dockerignore` 文件

```dockerignore
# 忽略编译产物
/target

# 忽略 Git 目录
.git
```

### 构建镜像

在 `Dockerfile` 所在的目录下，运行 `podman build` 命令来构建镜像
-t: tag your image

```sh
podman build -t hello-world-rust-server:v0.0.1 .
```

可以使用 `history` 查看镜像构建历史

```sh
podman history IMAGE
```

### 运行容器

用刚刚构建好的镜像来运行容器

下面的命令会以交互式方式运行我们的容器，可以看见程序的输出，容器停止后自动删除容器

```sh
podman run --rm -it -p 8080:3000 -e PORT=3000 hello-world-rust-server:v0.0.1
```
