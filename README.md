# Windows11-HyperIsland

**Release 1.1.0 · Windows 11 x64 · Publisher / 发布者：Escherichia30636**

[中文](#中文说明) · [English](#english)

## 中文说明

轻量的 Windows 11 顶部透明玻璃胶囊，显示时间、天气、Clash 延迟、消息和本机 Agent 状态。

### 下载与安装

从 [v1.1.0 Release](https://github.com/esch30636/Windows11-HyperIsland/releases/tag/v1.1.0) 下载 **Windows11-HyperIsland-1.1.0-x64.exe** 并运行。当前用户安装，无需管理员权限；使用 Windows 11 自带 .NET Framework，无需额外安装 Node.js、Python 或浏览器运行时。

已有 1.0.0 可直接运行新版更新，保留天气设置及缓存。要更新 Agent 提问与授权接入，请勾选“接入已有 Agent 配置”，安装程序先备份并保留无关设置与 Hook。DSH 及其他 Agent 可能需要自行重启或新开会话才能加载更新。

EXE 未做 Authenticode 数字签名，Windows 可能显示“未知发布者”。Escherichia30636 是发布署名，不代表代码签名证书。附件提供 SHA256SUMS.txt。

### 界面与逻辑

- 固定主屏顶部居中，516×34 DIP，各状态宽度一致，不可拖动，无托盘图标。透明玻璃配轻微模糊和曲面边缘高光。
- 空闲：**左侧 Clash 黑白猫头与延迟｜正中系统时间 HH:mm｜右侧温度和天气图标**，天气图标最右。
- 单个 Agent 任务显示“思考中”；多个显示“n个任务正在运行”，持续至真实结束或取消。
- 完成显示“Agent 名称 已完成”与最右绿色对勾 10 秒，再恢复仍在运行的任务或空闲界面。
- 提问显示白色无框“xxx向你提了个问题”，授权显示“xxx等待你授权”，最右橙色感叹号，处理或取消后更新。
- 微信/QQ Windows 通知显示应用图标与“你收到一条消息”，保留 10 秒。
- 应用图标纯白，不叠加数字或提示。右侧优先级：**提问 → 授权 → 完成 → 消息 → 运行 → 空闲**。并发完成和消息独立计时，被高优先级遮住且已过期的提醒不重播。
- **Alt+Z** 按一次隐藏，再按一次显示；隐藏后不挡住下面内容，新事件不会强行弹回。点击 Agent 图标只尝试激活已有应用，不代答或授权，不保证定位具体会话。

### Clash 延迟

通过已运行的 Clash Verge / Mihomo 的 `verge-mihomo` 本地命名管道，只读配置、代理与规则；不开 HTTP 控制端口，不修改代理或 TUN，不主动联网测速。

系统代理指向 Clash 或 TUN 开启时，显示默认策略所选节点最近缓存的延迟；两者均关闭显示“未开启”。无缓存显示“待测速”，失败记录显示“超时”。规则模式取 MATCH 默认策略，全局模式取 GLOBAL；不同网站可能命中其他规则节点。这是缓存测速值，不是每条连接的实时延迟。

仅空闲可见时每 30 秒读取本地缓存；配置/系统代理变化合并更新。任务或提醒显示、隐藏、锁屏和熄屏时停止读取。猫头为 Clash Verge 原始图标白色轮廓，并非 AI 重画。

### 通知与 Agent 接入

支持本机 ChatGPT/Codex、DeepSeek Harness、Claude Code、ZCode。Codex 依赖本机持久化日志；远程任务、ephemeral 会话、浏览器版 ChatGPT 及不写本地日志的会话不在自动检测范围。应用进程存在不代表任务运行。提问依赖结构化工具事件，不依据普通问号猜测；Agent 版本的事件格式差异可能影响接入。Claude/ZCode 同一会话内并行的同名工具授权可能合并关联。

微信/QQ 必须实际投递至 **Windows 通知中心**；仅任务栏闪动或应用自绘弹窗不能捕获。通知读取需要应用身份和你授予权限。可选身份使用开发包注册，要求已启用 Windows 开发者模式。安装程序不会修改开发者模式、证书信任或系统安全设置。可先安装其他功能，之后重跑启用通知身份，再从胶囊右键菜单授予通知访问。

### 使用、资源与隐私

右键可修改天气位置、更新天气、查看通知状态、隐藏或退出。位置手动保存，支持城市搜索或经纬度，不调用系统定位。天气每 30 分钟更新，离线保留上次结果；时间跟随系统，按分钟更新。

事件驱动和有限时长动画，无变化不重绘。锁屏、熄屏、会话断开或挂起时释放玻璃和绘图表面、停止分钟时钟，恢复后显示最新状态。不修改系统锁屏或电源超时。玻璃仍使用 Windows DWM，资源消耗因设备与场景而异。

设置、缓存、诊断保存在 `%USERPROFILE%\.dynamic-island`。不保存聊天正文；任务事件仅包含应用、状态、会话及请求标识。天气将设定区域经纬度发送给 Open-Meteo，城市搜索仅在操作时联网。安装包不含作者本机位置、缓存或 Agent 配置，也不向 GitHub 上传用户本机日志。

支持可选登录启动，重跑安装程序修改选项；可通过 Windows“已安装的应用”卸载，保留用户天气设置和诊断数据。

### 要求与权利

- Windows 11 x64，版本 22000 或更新；玻璃依赖 Windows 合成、驱动与透明设置。
- 天气来自 [Open-Meteo](https://open-meteo.com/)，区域模型不是某个门牌的实测温度。
- **仅二进制发布，应用源码继续保密**；GitHub 自动生成的源码压缩包只含仓库文档。
- 应用权利由 Escherichia30636 保留。第三方名称、商标和图标属各自权利人，无官方合作或背书，详见 NOTICE.md。

## English

A lightweight Windows 11 top-center glass capsule for the clock, weather, Clash latency, notifications and local agent states.

### Download and install

Download **Windows11-HyperIsland-1.1.0-x64.exe** from [v1.1.0 Release](https://github.com/esch30636/Windows11-HyperIsland/releases/tag/v1.1.0). Installs for the current user without administrator privileges. Uses Windows 11's built-in .NET Framework; no separate Node.js, Python or browser runtime is required.

Run the new installer to update 1.0.0; weather settings and cache remain. Select agent integration to update question/approval hooks. Setup backs up existing profiles and preserves unrelated configuration. DSH and other agents may need a restart or new session to load changes.

The EXE is not Authenticode-signed. Windows may show “Unknown publisher.” Escherichia30636 is the release attribution, not a certificate-backed identity. SHA256SUMS.txt is included.

### Interface and behavior

- Fixed top center on the primary display, 516×34 DIP in every state; no dragging or tray icon. Transparent glass, subtle blur and curved edge highlights.
- Idle: **Clash monochrome cat and latency on the left | system HH:mm clock centered | temperature and weather on the right**, weather icon at the far right.
- One task shows “思考中” (thinking); multiple tasks show “n个任务正在运行” (n tasks running), until actual completion or cancellation.
- Completion shows the agent name, “已完成” and a green check for 10 seconds, then returns to remaining work or idle.
- Questions show plain white “xxx向你提了个问题”; approvals show “xxx等待你授权”, with an orange exclamation mark at the far right until handled or cancelled.
- WeChat/QQ Windows notifications show a fixed message for 10 seconds. Status text currently uses Chinese.
- App icons remain plain white without badges. Priority: **question → approval → completion → message → running → idle**. Independent expiry deadlines prevent replay of expired reminders hidden by higher-priority content.
- **Alt+Z** toggles visibility. Hidden windows do not obstruct clicks and new events do not force them back. Clicking an agent icon only tries to activate its existing app; it never answers/approves and does not guarantee navigation to a specific session.

### Clash latency

Read-only access to the running Clash Verge / Mihomo `verge-mihomo` named pipe, with no HTTP controller, proxy/TUN changes or active network latency tests.

When the system proxy points to Clash or TUN is enabled, shows the default-policy node's latest cached delay. Both disabled shows “未开启” (off); no sample shows “待测速”; failed samples show “超时”. Rule mode follows MATCH, global mode follows GLOBAL. Individual destinations may use other rules; this is not live per-connection latency.

Reads local cache every 30 seconds only while idle and visible, with merged configuration/proxy-change updates. Stops during tasks/reminders, hiding and display suspension. The cat is extracted from the original Clash Verge icon, not AI-redrawn.

### Notifications and agents

Supports local ChatGPT/Codex, DeepSeek Harness, Claude Code and ZCode. Codex requires persistent local task logs; remote tasks, ephemeral sessions and browser ChatGPT are outside automatic detection. An application process alone does not count as a task. Questions use structured tool events rather than question-mark matching. Agent event-format differences may affect compatibility. Concurrent same-tool approvals within one Claude/ZCode session may be merged.

WeChat/QQ require actual **Windows notification-center notifications**; taskbar flashing and custom app popups are not captured. Notification access needs package identity and your permission. Optional unsigned development-package registration requires Developer Mode already enabled by you. Setup does not change Developer Mode, certificate trust or security settings. You may install other features first, enable identity later, then grant access from the capsule menu.

### Settings, resources and privacy

Right-click to set/refresh weather, inspect notifications, hide or exit. Location is manually saved through city search or coordinates; Windows location services are not queried. Weather updates every 30 minutes and keeps its last result offline. The clock follows Windows time, updating each minute.

Rendering is event-driven with finite animations. Lock, display-off, disconnect and suspend release glass/drawing surfaces and stop the clock, restoring the latest state afterward. No lock-screen or power timeout is changed. Glass still uses Windows DWM, with device- and scenario-dependent resource cost.

Settings, cache and diagnostics reside in `%USERPROFILE%\.dynamic-island`. Chat bodies are not stored. Task events contain app, state, session and request identifiers. Weather sends your configured area coordinates to Open-Meteo; geocoding runs only on search. No author's location, cache or agent profiles are packaged, and local user logs are not uploaded to GitHub.

Optional start-at-sign-in is available. Rerun Setup to change options or uninstall through Windows Installed apps; user weather settings and diagnostics are retained.

### Requirements and rights

- Windows 11 x64, build 22000 or later; glass depends on Windows composition, drivers and transparency settings.
- Weather: [Open-Meteo](https://open-meteo.com/). Area-model estimates are not street-address measurements.
- **Binary-only release; application source remains private.** GitHub-generated source archives contain repository documentation only.
- Application rights reserved by Escherichia30636. Third-party names and marks belong to their respective owners; no affiliation is implied. See NOTICE.md.
