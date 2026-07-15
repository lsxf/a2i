# A2iReply 快捷指令迁移说明

v1.11.0 已移除旧的 iOS 快捷指令和 ntfy `_reply` topic 方案。请删除原有的 `A2iReply` 快捷指令；GotMsg 不再订阅或使用 `_reply` topic。

新版本会在可回复的 ntfy 通知中直接附加一次性网页链接。iPhone 和 Android 都可点开网页输入回复，不需要额外配置。

完整说明见 [notification-reply.md](notification-reply.md)。
