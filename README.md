# MagicNet

MagicNet 是一个 Android root 网络治理模块，用于在设备侧统一接管和管理流量。

本仓库只是 KernelSU Modules Repo 分发镜像，不维护完整文档和源码。功能说明、更新日志、问题反馈和开发记录请看主仓库：

<https://github.com/LIghtJUNction/MagicNet>

## 安装

从本仓库 [Release 页面](https://github.com/KernelSU-Modules-Repo/MagicNet/releases) 下载 `MagicNet.zip`，在 KernelSU、APatch 或 Magisk 中安装并重启。

```bash
kam -S MagicNet
kam install MagicNet.zip
```

也可以直接安装主仓库 Git 构建版本：

```bash
kam install LIghtJUNction/MagicNet
```

## 能做什么

MagicNet 当前主线包括：

- `magicnet0` TUN 透明流量治理
- sing-box / mihomo 配置与运行管理
- WebUI、CLI 和 MCP 诊断入口
- 分应用规则、热点共享处理、VPN 共存辅助
- eBPF 路径检测与可用时启用，TUN 作为稳定兜底

更完整的使用方式以主仓库文档为准。

## 重要提示

- 不内置、分发或承诺任何第三方连通性资源。
- 请只导入合法、合规、自有的节点或配置。
- 如需排查 DNS 泄露，请先关闭 Android 系统的 Private DNS / 私人 DNS。
- 本镜像仓库的 release 可能受同步任务影响；主仓库始终是源码和文档的准确信息来源。

## 链接

- 主仓库：<https://github.com/LIghtJUNction/MagicNet>
- 完整 README：<https://github.com/LIghtJUNction/MagicNet/blob/main/README.md>
- 更新日志：<https://github.com/LIghtJUNction/MagicNet/blob/main/CHANGELOG.md>
- 问题反馈：<https://github.com/LIghtJUNction/MagicNet/issues>
