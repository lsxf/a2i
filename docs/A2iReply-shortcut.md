# A2iReply 快捷指令迁移说明

GotMsg v1.11.0 已移除旧的 iOS 快捷指令和 ntfy `_reply` topic 方案。请删除原有的 `A2iReply` 快捷指令；GotMsg 不再订阅或使用 `_reply` topic。

新版本把一次性回复地址设置为 Bark / ntfy 通知的点击地址或“回复”动作，不会在通知正文中重复显示。iPhone 和 Android 都可直接打开网页输入回复，无需另外安装快捷指令或修改现有 ntfy topic。

完整的安装要求、Shizuku / 无障碍配置、PIN 自动解锁和故障排查见 [通知远程回复](notification-reply.md)。
