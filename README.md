# MagicNet

MagicNet 是一个 Android root 网络模块，核心方向是实验性 eBPF 和内核级透明代理，在应用层之下接管设备流量。

本仓库只是 KernelSU Modules Repo 分发仓库。完整源码、文档、issue 和开发记录请看主仓库：

<https://github.com/LIghtJUNction/MagicNet>

## 安装

从本仓库 [Release 页面](https://github.com/KernelSU-Modules-Repo/MagicNet/releases)下载最新 `MagicNet.zip`，在 KernelSU、APatch 或 Magisk 中安装并重启。

```bash
kam -S MagicNet
kam install MagicNet.zip
```

也可以直接安装主仓库 Git 构建版本：

```bash
kam install LIghtJUNction/MagicNet
```

## 主仓库

- README：<https://github.com/LIghtJUNction/MagicNet/blob/main/README.md>
- 更新日志：<https://github.com/LIghtJUNction/MagicNet/blob/main/CHANGELOG.md>
