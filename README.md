<div align="center">
[![LatestRelease](https://img.shields.io/github/downloads/KernelSU-Modules-Repo/MagicNet/latest/MagicNet.zip?label=Downloads&logo=tailscale&color=31C2F2&style=flat-square)](https://github.com/KernelSU-Modules-Repo/MagicNet/releases)
[![TotalDownloads](https://img.shields.io/github/downloads/KernelSU-Modules-Repo/MagicNet/total?label=Total%20Downloads&logo=github&color=blue&style=flat-square)](https://github.com/KernelSU-Modules-Repo/MagicNet)
[![License](https://img.shields.io/github/license/LIghtJUNction/MagicNet?label=License&color=orange&style=flat-square)](https://github.com/KernelSU-Modules-Repo/MagicNet)
![MagicNet](https://github.com/user-attachments/assets/f46c5c92-27df-4edd-851d-cae77ebd8540)
</div>

# MagicNet
## 项目简介

MagicNet 是一个纯粹的透明代理，旨在让你和你的软件忘记/不知道你开启了代理。
为了实现以上目标：
1. 精准分流
2. 低内存占用（只有singbox能办到）
3. 开机自启动
4. 开启热点自动共享魔法
5. 和其他vpn软件共存

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
