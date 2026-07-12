# iOS 快捷指令 A2iReply — 自由输入回复

a2i 转发的通知在 iPhone 上**长按**出「回复」按钮后，会触发本快捷指令：弹出输入框让你打字，再把回复 POST 回 a2i 的反向 reply topic，a2i 收到后用 RemoteInput 回复原 App（短信/微信等）。

## 一次性配置

### 1. 记下 ntfy 配置
在 a2i「设置 → ntfy」记下一个已启用的 ntfy 配置：
- `server`：如 `https://ntfy.sh` 或自建 `https://ntfy.songer.eu.org`
- `topic`：如 `mytopic`
- `token`：若有鉴权则记下（自建 ntfy 常需要）

**反向 reply topic = `topic` + `_reply`**，例如 `mytopic_reply`。a2i 自动订阅这个派生 topic，快捷指令也往这里 POST。

### 2. iPhone 装 ntfy app
App Store 装 ntfy，订阅同 `mytopic`（用于收 a2i 转发的通知）。

### 3. 录制快捷指令 A2iReply
打开「快捷指令」app → 新建快捷指令，**命名为 `A2iReply`**（必须恰好此名，大小写一致）。

添加以下动作：

1. **要求输入**（Ask for Input）
   - 类型：文本
   - 提示：`输入回复内容`
   - 把输出命名为「回复内容」

2. **获取 URL 内容**（Get Contents of URL）
   - URL：`https://<server>/<topic>_reply`，例如 `https://ntfy.sh/mytopic_reply`
   - 展开「显示更多」
   - 方法：`POST`
   - 请求头（若 ntfy 有 token 才加）：
     - `Authorization` = `Bearer <你的token>`
   - 请求体：选 `JSON`，添加字段：
     - `message` = 「回复内容」（第 1 步的输出）
     - `title` = 「快捷指令输入」（Shortcut Input，即通知按钮 URL 传入的 `msgId=xxx`）

### 4. 允许运行
首次从通知触发可能需在「设置 → 快捷指令」允许「允许运行」/信任不受信任的快捷指令。

## 验证
1. 让 a2i 收一条短信（另一台手机发来）。
2. iPhone 收到 ntfy 通知 → 长按 → 点「回复」→ 快捷指令弹出 → 输入文字 → 自动发送。
3. 安卓端：a2i 收到回复 → 短信 App 自动回复该消息。
4. a2i「日志」页可见 `回复` 类型的 sent/failed 记录。

## 注意
- **公共 ntfy.sh 隐私**：reply topic 明文，任何人可读。生产建议自建 ntfy + token 鉴权。
- `title` 字段必须设为「快捷指令输入」（含 `msgId=` 前缀），a2i 靠它匹配原通知；删掉或改写会导致回复无法路由。
- 若原通知已被划掉/超 10 分钟，a2i 日志会记 `回复失败/原通知已失效`，属正常。
- 快捷指令名必须是 `A2iReply`，否则 a2i 通知按钮的 `shortcuts://run-shortcut?name=A2iReply` 触发不到。
