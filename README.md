<div align="center">
  
[![LatestRelease](https://img.shields.io/github/downloads/KernelSU-Modules-Repo/MagicNet/latest/MagicNet.zip?label=Downloads&logo=tailscale&color=31C2F2&style=flat-square)](https://github.com/KernelSU-Modules-Repo/MagicNet/releases)
[![TotalDownloads](https://img.shields.io/github/downloads/KernelSU-Modules-Repo/MagicNet/total?label=Total%20Downloads&logo=github&color=blue&style=flat-square)](https://github.com/KernelSU-Modules-Repo/MagicNet)
[![License](https://img.shields.io/github/license/LIghtJUNction/MagicNet?label=License&color=orange&style=flat-square)](https://github.com/KernelSU-Modules-Repo/MagicNet)
![MagicNet](https://github.com/user-attachments/assets/f46c5c92-27df-4edd-851d-cae77ebd8540)
</div>

# MagicNet
## 项目简介

MagicNet 是一个纯粹的透明代理，旨在让你和你的软件忘记/不知道你开启了代理。
它不是一个普通的 VPN App，而是一个运行在 Android Root 环境里的系统级网络模块：
安装后由模块在后台接管流量，把需要代理的连接送进代理内核，把不需要代理的连接继续直连。

为了实现以上目标，MagicNet 重点做了这些事：

1. 精准分流：尽量让国内、局域网、系统服务等流量直连，让需要代理的流量走代理节点。
2. 低内存占用：优先使用 sing-box / mihomo 这类适合常驻运行的代理内核，减少后台负担。
3. 开机自启动：设备重启后自动恢复透明代理，不需要每次手动打开 App。
4. 热点共享：手机开启热点后，热点客户端也可以复用手机上的代理能力。
5. VPN 共存：不占用 Android VPNService 通道，尽量减少和其他 VPN 类软件互相抢占的问题。
6. 订阅与规则：围绕常见代理订阅、规则分流、DNS 与 TUN 透明代理场景做默认集成。
7. MCP 服务器支持：默认关闭，需要 AI 辅助调试时再打开，让 AI 可以读取模块状态、日志和调试信息。
8. 模块化维护：使用 kam 构建模块，Release 仓库只负责分发，完整源码与问题反馈在源仓库维护。

如果你只想要一句话版：MagicNet 的目标是让 Android 设备在 Root 环境下获得“开机就有、应用无感、热点可共享”的透明代理体验。

## 功能介绍

### 透明代理

MagicNet 的核心是透明代理。普通代理通常需要你在每个 App 里手动设置 HTTP/SOCKS 代理，或者依赖一个 VPN App 接管流量；透明代理则是在系统网络层把流量自动转进代理内核。对浏览器、聊天软件、命令行工具、游戏和大多数普通应用来说，它们不需要知道代理存在。

### TUN 流量接管

模块通过 TUN 方式接管网络连接，让 TCP、UDP、DNS 等流量可以进入代理内核统一处理。这样可以覆盖更多应用，不依赖应用自己是否支持代理设置，也不会像传统 VPN App 一样占用 Android 的 VPNService 槽位。

### 规则分流

MagicNet 不追求“所有东西一股脑走代理”。更合理的做法是：

- 局域网、运营商网络、国内常见服务尽量直连，降低延迟和不必要的代理消耗。
- 需要代理的站点、服务或应用流量走代理节点。
- DNS 解析和最终出口保持一致，尽量减少 DNS 污染、解析错误和分流错配。

### 多内核思路

MagicNet 面向 sing-box / mihomo 等现代代理内核做集成。不同内核适合的配置格式、规则能力、运行特性不完全一样，模块会尽量把常用的透明代理、订阅、规则、启动和状态管理流程整理成普通用户可以直接使用的模块体验。

### 开机常驻

模块安装到 KernelSU、APatch 或 Magisk 后，会随系统启动。适合需要长期稳定代理环境的设备，比如备用机、开发测试机、随身热点机、平板或长期在线的 Android 设备。

### 热点共享

很多 VPN App 只能让手机自己走代理，热点连接进来的电脑、平板、游戏机仍然直连。MagicNet 的目标之一是让手机作为热点时，也能把热点客户端的流量转发到代理链路里，减少额外配置。

### 与 VPN App 共存

因为 MagicNet 是 Root 模块，不依赖 Android VPNService，所以理论上可以和部分 VPN、防火墙、抓包或局域网工具共存。实际效果仍取决于对方软件是否改路由、改 DNS、改 iptables/nftables，遇到冲突时建议一次只开一个网络接管类工具排查。

### MCP 服务器支持

MagicNet 特意新增了 MCP 服务器支持，默认关闭。它不是普通用户日常联网必须打开的功能，而是给 AI 辅助调试准备的接口。

现实世界的网络问题很复杂：订阅、节点、DNS、路由、TUN、热点转发、目标站风控、系统杀后台、不同 Android 版本差异，任何一个环节都可能导致“看起来像模块坏了”。人类手动处理这些日志和状态信息，速度和效率都很低；在需要排障时接入 AI，让 AI 直接读取结构化状态、日志和运行信息，是一个能节省很多时间的选择。

MCP 接入方式很简单：

- 默认保持关闭，需要调试时再手动开启。
- 电脑端使用 AI 工具时，可以通过 ADB 连接手机并做端口转发，让电脑上的 MCP 客户端访问手机里的 MagicNet MCP 服务。
- 如果手机本身安装了支持 MCP 的 agent 软件，也可以在手机本机连接。
- 通信方式采用 MCP Streamable HTTP，部署和接入都比较直接，不需要复杂的长连接网关。

这个功能适合“模块能启动但网络不对”“热点共享异常”“某些站点打不开”“DNS 或规则疑似错配”“需要快速看日志和运行状态”这类调试场景。平时只是正常使用透明代理，不需要开启 MCP。

### 适合谁

- 想让手机所有应用尽量无感使用代理的人。
- 想让 Android 热点共享代理给其他设备的人。
- 想减少 VPN App 后台、通知栏、误杀和手动开关的人。
- 熟悉或愿意学习 Root 模块、订阅、规则分流、DNS/TUN 基础概念的人。

### 不适合谁

- 完全没有 Root 环境，或不打算使用 KernelSU、APatch、Magisk 的用户。
- 只需要偶尔打开浏览器代理的人。
- 不愿意处理订阅质量、节点可用性、DNS、规则分流等网络问题的人。
- 需要商业软件级别客服、图形化配置面板和一键兜底的人。

## 基本使用流程

1. 准备一台已经安装 KernelSU、APatch 或 Magisk 的 Android 设备。
2. 从本仓库 Release 页面下载最新 `MagicNet.zip`。
3. 在 Root 管理器中安装模块并重启设备。
4. 按源仓库文档准备订阅、规则或本地配置。
5. 启动后先测试 Google、GitHub、ChatGPT 等目标站点，再测试国内站点、局域网和热点客户端。
6. 需要 AI 辅助排障时，再开启 MCP 服务器，并通过 ADB 端口转发或手机端 agent 接入。

透明代理模块的可用性很依赖节点质量、DNS、规则和设备系统环境。安装成功不等于所有网站都能稳定访问；如果某个站点打不开，需要区分是模块配置问题、节点问题、DNS 问题，还是目标网站对出口 IP 的风控问题。

## 常见排查方向

- 只有部分国外网站打不开：优先换节点，很多时候是出口 IP 质量或目标网站风控。
- 国内网站变慢：检查规则分流，确认国内流量没有被错误送进代理。
- App 能用但浏览器不能用，或反过来：检查 DNS、IPv6、UDP、应用自己的代理设置和系统网络缓存。
- 热点客户端没网：检查热点转发、系统防火墙、客户端网关/DNS，以及模块是否真的接管了热点流量。
- 重启后失效：检查模块是否被 Root 管理器禁用，代理内核是否启动，日志里是否有配置解析错误。
- 和其他 VPN/防火墙冲突：先关闭其他会改路由、改 DNS、改 iptables/nftables 的软件，确认 MagicNet 单独运行是否正常。

## 网络小白推荐阅读

如果你刚接触代理、DNS、TCP/IP、路由、NAT、网关、HTTP、TLS 这些词，建议先看一本通俗但很扎实的入门书：

- [《网络是怎样连接的》PDF](https://raw.githubusercontent.com/tongxurt/pdfs/master/%E7%BD%91%E7%BB%9C%E6%98%AF%E6%80%8E%E6%A0%B7%E8%BF%9E%E6%8E%A5%E7%9A%84_%E6%88%B7%E6%A0%B9%E5%8B%A4.pdf)

这本书适合先建立直觉：浏览器输入网址之后，DNS 如何解析，TCP 如何连接，路由器和运营商网络如何转发，服务器如何返回数据。理解这些之后，再看 MagicNet 里的 TUN、DNS、规则分流、透明代理、热点转发，会少很多“玄学网络问题”。

## 核心理念

- 保持模块尽可能精简、可理解、可维护，同时让普通用户也能快速获得可用的透明代理体验。
- 最简单，可用的版本（不到50行，请翻历史，最开始最简陋的版本是我人工编写的）

## 人工智能使用声明

- 我小半年没更新了，因为我懒，多亏了gpt5.5，不然这项目可能得等到年底才会更新。
- 我欢迎贡献代码，但是禁止使用以下模型（或者你声明你人工检查过）：
- minimax/文心/豆包/以及任何网页版/手机版对话AI生成的代码
- 其余不受限制

## 快速开始

- 请从 Release 页面下载最新 `MagicNet.zip`，在 KernelSU、APatch 或 Magisk 中安装并重启设备。

- 详细文档、源码与问题反馈请访问源仓库：
- https://github.com/LIghtJUNction/MagicNet

## 标准化模块开发工具

[kam](https://github.com/MemDeco-WG/Kam)
人生苦短，安装这个技能让ai帮你学
```bash
npx skills add MemDeco-WG/Kam # -g ：全局，如果你下载了bun，可以用bunx
```

本项目是
kam模块构建的模范项目
本仓库由kam 初始化

使用kam构建模块：

```bash
kam init . --repo-mode reference
# 意思是只放一个同步用的工作流和module.json
```
本体仓库：
```bash
kam init -i  # --repo-mode full 这是默认的
# 给人类设计的交互式新建命令
```
