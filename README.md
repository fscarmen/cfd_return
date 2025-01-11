# 【CFD 反向回源一键脚本】

- 一个基于 Cloudflare Tunnel 的双向流量回源工具，支持 CentOS、Debian、Ubuntu、Alpine 和 OpenWRT 系统。

* * *

# 目录

- [1. 教程](README.md#1教程)
- [2. 特点](README.md#2特点)
- [3. 支持的操作系统和架构](README.md#3支持的操作系统和架构)
- [4. 安装方法](README.md#4安装方法)
- [5. 卸载方法](README.md#5卸载方法)
- [6. 命令行参数](README.md#6命令行参数)
- [7. 使用示例](README.md#7使用示例)
* * *
## 1. 教程
- 博客教程: https://www.fscarmen.com/2025/01/gost-argo.html
- 视频教程:

## 2. 特点
- 突破公网入口限制：传统 CDN 需要 VPS 具有公网 IP，而本工具借助 Cloudflare Tunnel，实现了内网穿透，无需公网 IP 即可接入 CDN。
- 自动优选 cloudflared 接入 IP: 使用热心网友 cf中转ip群群主提供的玩具 cfd，从多个候选的 endpoint（包括 region1.v2.argotunnel.com、region2.v2.argotunnel.com、us-region1.v2.argotunnel.com、us-region2.v2.argotunnel.com 等）中，这些 endpoint 可能包含多个 IPv4 和 IPv6 地址，工具选出延迟最小的接入 IP。
- 应用场景广泛：除了传统的 VPS 外，你还可以在各种容器、游戏平台甚至家庭网络中部署本工具，实现服务的全球加速访问。
- 无需额外优选：由于 Cloudflare 的线路质量通常很好，因此使用本工具时无需进行额外的网络优选，即可享受稳定的访问速度。
- 轻量运行：本工具近乎 0 依赖，不需要处理复杂的证书和配置问题，安装和使用都非常简单。

## 3. 支持的操作系统和架构

| | 系统 | 架构 |
| -- | -- | -- | 
| 服务端 | CentOS,Debian,Ubuntu,OpenWRT | amd64 (x86_64),amd64 (x86_64),armv7 |
| 客户端 | CentOS,Debian,Ubuntu,Alpine | amd64 (x86_64),amd64 (x86_64),armv7 |

## 4. 安装方法

### 4.1 服务端安装

#### 4.1.1 交互式安装：

```bash
bash <(wget -qO- https://raw.githubusercontent.com/fscarmen/cfd_return/main/cfd_return.sh)
```

#### 4.1.2 快捷参数安装：

```
bash <(wget -qO- https://raw.githubusercontent.com/fscarmen/cfd_return/main/cfd_return.sh) \
  -s \
  -p server-origin-port \
  -d your-domain.com \
  -w your-ws-path \
  -t 4 \
  -a your-cloudflare-auth
```

### 4.2 客户端安装

#### 4.2.1 交互式安装：

```
bash <(wget -qO- https://raw.githubusercontent.com/fscarmen/cfd_return/main/cfd_return.sh)
```

#### 4.2.2 快捷参数安装：

```
bash <(wget -qO- https://raw.githubusercontent.com/fscarmen/cfd_return/main/cfd_return.sh) \
  -c \
  -r remote-socks5-port \
  -d your-domain.com \
  -w your-ws-path
```

## 5. 卸载方法

```
bash <(wget -qO- https://raw.githubusercontent.com/fscarmen/cfd_return/main/cfd_return.sh) -u
```

## 6. 命令行参数

| 参数 | 说明                    | 使用场景       |
| ---- | ----------------------- | -------------- |
| -h   | 显示帮助信息            | 服务端和客户端   |
| -u   | 卸载服务端和客户端      | 服务端和客户端   |
| -w   | WebSocket 路径          | 服务端和客户端 |
| -d   | Cloudflare Tunnel 域名  | 服务端和客户端 |
| -s   | 安装服务端              | 服务端         |
| -a   | Cloudflare Tunnel json 或 token 认证 | 服务端         |
| -t   | Cloudflared 优选 IP 列表 [4,6,d]，默认为双栈 d | 服务端 |
| -p   | 服务端端口              | 服务端         |
| -n   | 显示客户端安装命令      | 服务端         |
| -c   | 安装客户端              | 客户端         |
| -r   | 映射到服务端的 SOCKS5 端口  | 客户端         |

## 7. 使用示例

### 7.1 服务端完整安装示例：

```
bash <(wget -qO- https://raw.githubusercontent.com/fscarmen/cfd_return/main/cfd_return.sh) \
  -s \
  -p 20000 \
  -d cfd.example.com \
  -w 3b451552-e776-45c5-9b98-bde3ab99bf75 \
  -t 4 \
  -a eyJhIjoiOWN...
```

### 7.2 客户端完整安装示例：

```
bash <(wget -qO- https://raw.githubusercontent.com/fscarmen/cfd_return/main/cfd_return.sh) \
  -c \
  -r 30000 \
  -d cfd.example.com \
  -w 3b451552-e776-45c5-9b98-bde3ab99bf75
```

### 7.3 查看客户端安装命令：

```
bash <(wget -qO- https://raw.githubusercontent.com/fscarmen/cfd_return/main/cfd_return.sh) -n
```

### 7.4 卸载所有组件：

```
bash <(wget -qO- https://raw.githubusercontent.com/fscarmen/cfd_return/main/cfd_return.sh) -u
```