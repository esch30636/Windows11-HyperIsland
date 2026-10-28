# Windows11-HyperIsland

**Release 1.0.0 · Windows 11 x64 · Publisher / 发布者：Escherichia30636**

[中文](#中文说明) · [English](#english)

## 中文说明

Windows11-HyperIsland 是一个轻量的 Windows 11 顶部胶囊：透明玻璃背景、轻微模糊和曲面高光，空闲时显示时间天气，有消息或 Agent 任务时切换为应用状态。

### 下载与安装

从 [Releases](https://github.com/esch30636/Windows11-HyperIsland/releases) 下载 **Windows11-HyperIsland-1.0.0-x64.exe**，运行后选择安装选项。安装到当前用户目录，无需管理员权限。Windows 11 自带的 .NET Framework 即可运行，无需 Node.js、Python 或浏览器运行时。

首版 EXE **未做 Authenticode 数字签名**，Windows 可能显示“未知发布者”。Escherichia30636 是应用元数据与本项目的发布署名，不代表已取得代码签名证书。请只使用本仓库 Release 附件并核对 SHA-256。

### 功能

- 透明、局部轻模糊的玻璃材质，增强曲面边缘；固定主屏顶部居中，不可拖动。
- 空闲常驻：左侧系统时间，精确到分；右侧温度，最右侧黑白天气图标。
- 微信 / QQ 的 Windows 系统通知显示应用图标与“你收到一条消息”，保留 10 秒。
- ChatGPT/Codex、DeepSeek Harness、Claude Code、ZCode 的本机任务：运行时显示“思考中”；成功结束后显示“已完成”及绿色对勾，保留 10 秒。
- **Alt+Z** 按一次隐藏、再按一次显示；隐藏后不挡住下层内容，新消息也不会强行弹回。
- 无系统托盘图标。只在内容或显示状态变化时重绘；动画结束即停止。

### 通知与 Agent 接入

微信 / QQ 必须实际投递到 **Windows 通知中心**；仅任务栏图标闪动或应用自绘弹窗不能被此接口捕获。系统通知读取还需要应用身份和你主动授予通知访问权限。

由于首版没有代码签名证书，可选的系统通知身份使用 Windows 开发包注册，要求你已自行启用 Windows 开发者模式。安装程序不会自动更改开发者模式、证书信任或系统安全设置。未启用时可以先安装时间、天气和 Agent 状态功能，之后重新运行安装程序启用系统通知，再从胶囊右键菜单授予通知访问。

安装时可选择接入已存在的本机 Agent 配置。安装程序会先备份配置，再保留无关设置和 Hook。Claude Code、ZCode 和 DeepSeek Harness 的已有会话可能需要正常新开会话 / 重启对应 Agent 才加载新配置。Codex 使用本机持久化任务日志；远程任务、`ephemeral` 会话、浏览器版 ChatGPT 和不写本地日志的会话不在当前自动检测范围。应用进程存在本身不代表任务正在执行。

### 使用与设置

右键胶囊可设置天气位置、更新天气、查看通知状态、隐藏或退出。天气位置手动保存，可搜索城市或输入区域经纬度；**不调用系统定位**。天气默认每 30 分钟联网更新，断网时保留上次结果。时间直接跟随本地系统时间，不单独联网校时。

设置和缓存保存在 `%USERPROFILE%\.dynamic-island`。不会保存聊天正文；任务 Hook 只传递应用、状态和会话标识。天气请求将你设置的区域经纬度发送至 Open-Meteo；城市搜索只在点击搜索时请求。不会将本机配置或日志上传到 GitHub。

安装程序提供“登录后自动启动”选项。再次运行安装程序可修改安装 / 集成选项，也可通过 Windows“已安装的应用”卸载。卸载保留用户天气设置和诊断数据。

### 要求、限制与授权

- Windows 11 x64，版本 22000 或更新；透明效果依赖 Windows 合成能力，建议启用系统透明效果。
- 天气来自 [Open-Meteo](https://open-meteo.com/)，区域模型结果不是某一门牌的实测气温。
- 本项目为**仅二进制发布**，暂不公开应用源码。GitHub 自动生成的源码压缩包只包含仓库文档，不包含应用工程。
- 应用和源码的权利由 Escherichia30636 保留；各应用名称、商标和标志属于其各自权利人，未表示官方合作。

## English

Windows11-HyperIsland is a lightweight, fixed top-center capsule for Windows 11. It combines transparent glass, subtle background blur and curved highlights with a minute-accurate system clock, weather, notifications and local agent task states.

### Download and install

Download **Windows11-HyperIsland-1.0.0-x64.exe** from [Releases](https://github.com/esch30636/Windows11-HyperIsland/releases), run it and choose the installation options. It installs for the current user without administrator privileges. The .NET Framework included with Windows 11 is sufficient; Node.js, Python and a browser runtime are not required.

This first release is **not Authenticode-signed**. Windows may show “Unknown publisher.” Escherichia30636 is the publisher attribution in the application metadata, not a claim of certificate-backed identity. Obtain the binary from this repository's release assets and verify its SHA-256 checksum.

### Features

- Transparent glass with localized subtle blur and curved edge highlights; fixed at the top center of the primary display.
- Resident idle view: local system time on the left, temperature and a monochrome weather icon at the far right.
- WeChat / QQ Windows notifications show the application icon and a fixed message for 10 seconds.
- Local ChatGPT/Codex, DeepSeek Harness, Claude Code and ZCode tasks show a thinking state until they end. Successful completion shows a green check for 10 seconds.
- **Alt+Z** toggles visibility. A hidden capsule does not cover underlying content and new events do not force it to reappear.
- No tray icon. Content-driven rendering and finite animations rather than continuous application redraw loops.

### Notifications and agent integrations

WeChat and QQ must deliver actual **Windows notification-center notifications**. Taskbar flashing and application-owned popups are not captured. Reading system notifications requires package identity and notification access granted by you.

Because this release has no code-signing certificate, optional notification identity uses development-package registration and requires Windows Developer Mode to have been enabled by you. Setup does not modify Developer Mode, certificate trust or security settings. You can install clock, weather and agent status functionality first, rerun Setup later to enable notification identity, and then grant notification access from the capsule's context menu.

Setup can optionally integrate with existing local agent profiles. It backs up configuration before preserving unrelated settings and hooks. Existing Claude Code, ZCode and DeepSeek Harness sessions may need a new session or an agent restart to load integrations. Codex detection uses persistent local task logs; remote tasks, ephemeral sessions, browser-based ChatGPT and sessions without local logs are not automatically detected. Merely running an application does not count as an active task.

### Settings and privacy

Right-click the capsule to configure weather location, refresh weather, inspect notifications, hide or exit. Weather location is stored manually using a city search or coordinates; **Windows location services are not queried**. Weather normally updates every 30 minutes and retains the last result when offline. The clock follows local Windows time without separate network time requests.

Settings and cache reside in `%USERPROFILE%\.dynamic-island`. Chat message bodies are not saved. Task hooks send only application, state and session identifiers. Weather requests send your configured area coordinates to Open-Meteo; geocoding is requested only when you search. Local settings and logs are not uploaded to GitHub.

Setup includes an optional start-at-sign-in setting. Rerun Setup to change installation / integration options, or uninstall through Windows Installed apps. User weather settings and diagnostic data are retained on uninstall.

### Requirements, limitations and rights

- Windows 11 x64, build 22000 or later. Glass depends on Windows composition capabilities; system transparency effects should be enabled.
- Weather data: [Open-Meteo](https://open-meteo.com/). Area-model estimates are not measurements at a particular street address.
- This is a **binary-only release**. Application source is not public. GitHub's automatically generated source archives contain repository documentation only.
- Application rights are reserved by Escherichia30636. Third-party product names, trademarks and logos belong to their respective owners; no official affiliation is implied.
