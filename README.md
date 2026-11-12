# Weissach

Weissach 以保时捷研发中心命名，是一个独立悬浮在 macOS 桌面的编码搭档。十款原创像素车型，用五种动画状态陪伴编码。主窗口分为四个 tab：**车库**（车型、演示、实时会话）、**配置**（客户端接入）、**Token 用量**（本机用量统计）、**赛道**（圈数、里程与出勤统计）。

支持 18 个客户端：Claude Code、Codex、GitHub Copilot、Cursor、Gemini CLI、Antigravity CLI、CodeBuddy、Tencent WorkBuddy、Qoder、Qoder CN、QoderWork、Qwen Code、Kimi CLI、OpenCode、Pi Agent、Oh My Pi、Hermes、OpenClaw。Weissach 只观察会话状态，所有权限确认和问题仍由原客户端处理。

## 截图

<p align="center"><img src="screenshots/car.png" width="256" alt="悬浮在桌面上的座驾"></p>

**车库**：十款车型，随里程逐步解锁。

![车库里的经典收藏](screenshots/garage.png)

**配置**：检测本机已安装的客户端，逐个接入或移除。

![配置 tab](screenshots/config.png)

**Token 用量**：只读取本机记录，按天统计。

![Token 用量 tab](screenshots/token.png)

**赛道**：圈数、行驶时长、里程与出勤。

![赛道 tab](screenshots/track.png)

## 下载

**[下载 Weissach-1.0.0-mac-universal.dmg](https://github.com/qubyyang/Weissach-Release/releases/latest/download/Weissach-1.0.0-mac-universal.dmg)**

历史版本见 [Releases](https://github.com/qubyyang/Weissach-Release/releases)。

- 系统要求：macOS 14 或更新版本
- 架构：Universal（Apple Silicon 与 Intel）
- 安装包已用 Developer ID 签名并通过 Apple 公证，可以直接打开

## 安装

1. 打开 DMG，把 `Weissach.app` 拖入 `/Applications`。
2. 启动 Weissach，在「配置」tab 里为要接入的客户端点「查看配置 → 备份并安装」。

建议先把 App 移入 `/Applications` 再配置接入，这样写入各客户端的命令路径不会随 App 位置变化。

## 校验

```sh
shasum -a 256 Weissach-1.0.0-mac-universal.dmg
```

1.0.0 的 SHA-256：

```
cda78b5108c6967e1cad42c948176f844bfd620d945ac135d3c0302ac62c2d3c
```

## 使用

- 拖动座驾改变位置，双击打开车库，右键切换车型、演示状态或隐藏座驾。
- 菜单栏汽车图标可打开车库、显示或隐藏座驾、退出；有会话待回应或中断时，图标旁会出现色点和数量。
- 全局快捷键「跳到待处理会话」默认 `⌃⌥⌘J`，可在主窗口底栏修改或关闭。

## 数据

数据保存在本机 `~/Library/Application Support/Weissach`。卸载时删除 App 和这个目录即可。

## 反馈

问题和建议请提交到 [Issues](https://github.com/qubyyang/Weissach-Release/issues)。
