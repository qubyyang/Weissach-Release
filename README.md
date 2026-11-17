# Weissach

Weissach 以保时捷研发中心命名，是一个独立悬浮在 macOS 桌面的编码搭档。十款原创像素车型，用五种动画状态陪伴编码。主窗口分为四个 tab：**车库**（车型、演示、实时会话）、**配置**（客户端接入）、**Token 用量**（本机用量统计）、**赛道**（圈数、里程、出勤与进站统计）。

支持 18 个客户端：Claude Code、Codex、GitHub Copilot、Cursor、Gemini CLI、Antigravity CLI、CodeBuddy、Tencent WorkBuddy、Qoder、Qoder CN、QoderWork、Qwen Code、Kimi CLI、OpenCode、Pi Agent、Oh My Pi、Hermes、OpenClaw。Weissach 只观察会话状态，所有权限确认和问题仍由原客户端处理。

## 截图

<p align="center"><img src="screenshots/car.png" width="256" alt="悬浮在桌面上的座驾"></p>

**车库**：十款车型，随里程逐步解锁。

![车库里的经典收藏](screenshots/garage.png)

**配置**：检测本机已安装的客户端，逐个接入或移除。

![配置 tab](screenshots/config.png)

**Token 用量**：只读取本机记录，按天统计。

![Token 用量 tab](screenshots/token.png)

**赛道**：圈数、行驶时长、里程与出勤；切到「进站」看会话等了你多久。

![赛道 tab](screenshots/track.png)

## 下载

**[下载 Weissach-1.5.0-mac-universal.dmg](https://github.com/qubyyang/Weissach-Release/releases/latest/download/Weissach-1.5.0-mac-universal.dmg)**

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
shasum -a 256 Weissach-1.5.0-mac-universal.dmg
```

1.5.0 的 SHA-256：

```
d05325e646f1ddd3b158f4d856928dbaeec3d5b03dc7631a5dd6f90071ac6a3d
```

## 使用

- 拖动座驾改变位置，双击打开车库，右键切换车型、演示状态或隐藏座驾。
- 菜单栏汽车图标可打开车库、显示或隐藏座驾、退出；有会话待回应或中断时，图标旁会出现色点和数量，有会话跑完还没看时另有一个绿点。
- 等你回应、中断或跑完的会话会一直显示，并标出已经等了多久，直到你处理它或它确实结束；关掉终端标签页或结束会话后，它会在约 10 秒内消失。
- 有会话等你回应或中断时，Weissach 发一条系统通知，点击通知就跳到那个会话。几个会话同时需要你时合并成一条，全部处理完后通知自动撤掉。会话跑完的提醒默认关闭，两个开关都在「配置」tab 的「提醒」里。第一次提醒时 macOS 会问是否允许 Weissach 发通知；专注模式和系统的通知设置照常生效。
- 跳转（点击座驾标签或菜单里的会话、按快捷键、点击通知）会尽量到具体的位置：Terminal、iTerm2 和 Ghostty 到标签页，Xcode 和 VS Code 到项目窗口，WorkBuddy 和 GitHub Copilot App 到会话，其他 App 只切到前台。「配置」tab 的「跳转」一节列出本机每个目标的级别。第一次跳到 Terminal、iTerm2、Ghostty 或 Xcode 时，macOS 会问是否允许 Weissach 控制它；拒绝后只切到 App。Weissach 不申请辅助功能权限。
- 全局快捷键「跳到待处理会话」默认 `⌃⌥⌘J`，可在主窗口底栏修改或关闭。通过 Weissach 跳转到一个会话即视为已看；也可以在菜单栏或座驾的右键菜单里选择「全部标为已看」。
- 「赛道」tab 顶部可以在「圈」和「进站」之间切换。会话等你回应、中断或跑完时算一次进站，到你回去为止。「进站」一边显示次数、中位时长、最长一次和未回应的次数，与上一个同样长的时段的对比，以及趋势、按类型和按客户端的拆分。「该你回应」（待回应和中断）与「跑完」分开统计；时长只算你回去了的进站，关掉会话或退出 Weissach 而结束的计入「未回应」。「跑完」的时长包含你不在电脑前的时间，只适合看趋势。
- 有新版本时，主窗口底栏和菜单栏菜单里会出现「有新版本 → 下载」，点击打开下载页。Weissach 不会自己下载或安装。

## 数据

数据保存在本机 `~/Library/Application Support/Weissach`。卸载时删除 App 和这个目录即可。

进站统计读的是本机的进站记录，每行只有客户端、开始时间、类型、等待时长和结束方式；它从 1.1 起就在记，1.5 没有新增任何记录的数据。在「配置」tab 清空里程记录时一并删除。

从 1.4 起，为了跳到对应的项目窗口，接入的 hook 会把会话的完整工作目录放进实时事件。它只存在于待读取的事件文件（Weissach 读取后即删除；Weissach 没在运行时，最后一批事件会留到下次读取）和 Weissach 的内存中，不写入任何记录，不显示在界面上，不进通知，不联网。

通知含状态、项目目录名、会话标题和客户端名，与座驾上显示的相同；它们由 macOS 的通知中心保存，直到会话被处理或你清除通知。

检查更新是 Weissach 唯一的联网行为：启动时和每天一次，向 GitHub 读取最新版本号。请求不含任何本机信息；GitHub 会看到这台电脑的 IP 地址和 Weissach 的版本号。在「配置」tab 关闭「自动检查更新」后不再发出任何请求。

## 反馈

问题和建议请提交到 [Issues](https://github.com/qubyyang/Weissach-Release/issues)。
