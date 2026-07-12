# GotMsg ·有消息

> **闭源声明**：GotMsg 为闭源软件，源码不公开。本仓库仅作为**发布页**，提供 README 文档与 Release APK 下载。License: All Rights Reserved。

把安卓手机上的通知（短信、验证码、电话、微信、QQ、Telegram）实时转发到 iOS / Android / 鸿蒙等接收端。

适用于把安卓备机的消息同步到 iPhone 或其他安卓 / 鸿蒙手机，不漏验证码、不漏重要聊天。

![GotMsg 设置页](screenshots/overview.png)

---

## 一、五分钟上手

### 1. 安装
从 [Releases](../../releases) 下载最新 APK，安装到安卓手机（需 Android 14 / API 34+）。

### 2. 选一个推送通道
推荐三选一：

| 接收设备 | 推荐通道 | 难度 |
|---|---|---|
| iPhone / iPad | **Bark** | ⭐ 最简单 |
| 安卓手机 | **ntfy** | ⭐ 推荐开源 |
| 鸿蒙手机 | **Meow** | 鸿蒙专属 |

打开 GotMsg -> 「设置」-> 选对应通道 -> 点右上角 **i** 按钮 -> 按弹窗步骤配 -> 点该行「发送」测试。

### 3. 授权通知监听
首页会提示「需要授权通知监听」。点击「前往系统授权」，在系统的通知访问设置中开启 GotMsg。

### 4. 开启转发
首页打开「通知转发」开关。安卓收到通知后按配置自动推送到各通道。

---

## 二、推送通道配置详解

每条配置都可独立勾选/删除/排序/测试。点「添加」时建议每条都先「发送」测试一次。

### 2.1 Bark（iOS / iPadOS）

[Bark](https://github.com/Finb/Bark) 是 iOS 上最轻量的推送方案，复制地址即用，**推荐所有 iOS 用户首选**。

**配置步骤**：
1. iPhone / iPad 上安装 Bark，首次打开允许通知权限。
2. 复制 Bark 首页的推送地址，形如 `https://api.day.app/你的Key`。
3. GotMsg「设置 -> Bark 服务器 -> 添加」：
   - **名称**：随意，例如「我的 iPhone」
   - **服务器地址**：`https://api.day.app`（自建则填自建地址）
   - **Device Key**：Bark 地址中 `/` 后面的那段
4. 保存后点「发送」测试；iPhone 收到「GotMsg 测试」即成功。

**为什么推荐 Bark**：iOS 上点击 Bark 通知可一键跳转到微信、QQ、Telegram 对应 App；iOS 14+ 通知体验最自然；Bark 服务器在中国大陆可直接访问。

### 2.2 ntfy（Android / iOS / 网页）

[ntfy](https://ntfy.sh) 是开源的 HTTP pub-sub 通知服务，**支持 Android、iOS 和网页端**，无需注册项目。

**配置步骤**：
1. 接收端安装 ntfy：
   - Android：[Google Play](https://play.google.com/store/apps/details?id=io.heckel.ntfy) / [F-Droid](https://f-droid.org/en/packages/io.heckel.ntfy/) / [GitHub](https://github.com/binwiederhier/ntfy)
   - iOS：[App Store](https://apps.apple.com/us/app/ntfy/id1625396347)
2. 打开 ntfy -> 添加订阅。服务器填 `https://ntfy.sh`（或自建地址）；Topic 用一串**随机难猜的名字**（如 `gotmsg_a8f3d2`）。
3. GotMsg「设置 -> ntfy 转发 -> 添加」：
   - **服务器**：与接收端完全一致
   - **Topic**：与接收端完全一致
   - **Token**：仅自建服务且启用了鉴权时填
4. 保存后点「发送」测试；接收端收到「GotMsg 测试」即成功。

> **安全提示**：公共 topic 谁知道名字就能订阅或发送。Topic 名**不要用**手机号、姓名、邮箱等可猜信息。

### 2.3 Meow（鸿蒙 / HarmonyOS）

Meow 是鸿蒙手机的推送接收方案。GotMsg 按你填写的 Meow 接口地址和 Device Key 发出 HTTP 请求即可。

**配置步骤**：
1. 鸿蒙手机上安装 Meow，确认 Meow 自身能正常接收推送。
2. 在 Meow 里找到**推送接口地址**和对应的 **Device Key / Token**。
3. GotMsg「设置 -> Meow 转发 -> 添加」：
   - **名称**：按鸿蒙设备填写（方便区分多台）
   - **服务器地址**：Meow 给出的完整 API 地址
   - **Device Key**：Meow 给你的设备 Key（**不是**鸿蒙锁屏密码、华为账号密码）
4. 保存后点「发送」测试；鸿蒙手机收到「GotMsg 测试」即成功。

> 失败排查：检查 Meow 接口地址是否完整、Key 是否复制完整、鸿蒙手机是否允许 Meow 通知。

### 2.4 电邮转发

通过 SMTP 把通知发到邮箱（**适合无手机接收的场景**，如仅在桌面/平板查看）。

**配置步骤**：
1. 准备一个 SMTP 邮箱（QQ/163/Gmail/Outlook 都可），**开启 SMTP 服务并生成授权码**（不是登录密码）。
   - QQ：设置 -> 账户 -> POP3/IMAP/SMTP/Exchange/CardDAV/CalDAV服务 -> 开启 SMTP -> 生成授权码
   - 163：设置 -> POP3/SMTP/IMAP -> 开启 SMTP -> 设置授权码
   - Gmail：账户 -> 安全性 -> 两步验证 -> 应用专用密码
2. GotMsg「设置 -> 电邮转发 -> 添加」：
   - **名称**：随意
   - **服务器（SMTP 主机）**：`smtp.qq.com` / `smtp.163.com` / `smtp.gmail.com` 等
   - **端口**：`465`（推荐，隐式 SSL）或 `587`（STARTTLS）
   - **账号**：完整邮箱地址
   - **授权码 / 密码**：上一步生成的授权码
   - **发件人**：通常与账号相同
   - **收件人**：接收通知的目标邮箱
3. 保存后点「发送」测试；收件人收到「GotMsg 测试」即成功。

> **国内邮箱推荐端口 465**（QQ/163 均支持）。Gmail 需要应用专用密码而不是账户密码。

### 2.5 断网短信兜底

**当安卓手机没有网络时**，把重要通知（验证码、来电）通过 **SIM 卡短信** 发到另一台手机（通常是你的 iPhone）。需要安卓卡里还有短信套餐余量。

**配置步骤**：
1. 在 GotMsg「设置 -> 短信兜底」点「授予短信权限」（安卓系统权限）。
2. 点「添加」输入**目标手机号**（如 iPhone 号，接收端是另一台手机，**不是** GotMsg 本身）。
3. 选运营商：
   - 选了「自动识别」：GotMsg 会发免费查询短信给运营商服务号，解析回执获取余量。
   - 选了「手动额度」：在「手动短信额度」填入当前套餐短信条数，每次发短信后自动减 1。
4. 当余量 ≤ 5 时自动暂停，下次打开 App 提醒续费。
5. 频率限制：每 5 分钟最多发 1 条（避免刷屏），同一条通知 5 分钟内不重复。

> **适用场景**：安卓手机没 WiFi 时，验证码不会丢，漏不了重要登录。

---

## 三、自建推送服务（可选）

所有通道都支持自建，更好、更私密、可控。

### 3.1 自建 Bark 服务器

GotMsg 默认用 Bark 官方服务器（`https://api.day.app`），免费够用。自建适合追求完全控制。

**Docker 一键部署**（推荐）：
```bash
docker run -d --name bark --restart=unless-stopped \
  -p 8080:8080 \
  -v /var/lib/bark:/data \
  finab/bark-server
```

然后用 Nginx Proxy Manager 加 HTTPS 域名。详细三种方案对比请看 [Bark 官方文档](https://github.com/Finb/Bark)。

**GotMsg 配置**：服务器地址填 `https://你的域名.com`（不要 `/push` 后缀），Device Key 填你在自建 Bark 上创建的 Key。

### 3.2 自建 ntfy 服务器

[ntfy](https://ntfy.sh) 是为自建设计的，**比 Bark 还简单**--官方直接提供 Docker 一行启动：

```bash
docker run -d --name ntfy --restart=unless-stopped \
  -p 80:80 \
  -v /var/lib/ntfy:/var/lib/ntfy \
  binwiederhier/ntfy serve
```

推荐加 Nginx 反代上 HTTPS 域名。完整文档：[docs.ntfy.sh](https://docs.ntfy.sh/install/)。

**GotMsg 配置**：服务器地址填 `https://ntfy.你的域名.com`，Topic 照旧。

### 3.3 自建 Meow 服务器
Meow 是鸿蒙客户端，服务端一般用 Meow 自带的。GotMsg 端无需配置服务端，只需填 Meow 给你的接口地址 + Key。

---

## 四、ntfy 通知回复（iPhone 自由输入回复）

v1.10.2 起，ntfy 转发的通知支持在 iPhone 上**长按 ->「回复」-> 用 iOS 快捷指令自由输入文字 -> 自动回复回原 App**（短信/微信等带通知快捷回复的 App）。

配置步骤见 [docs/A2iReply-shortcut.md](docs/A2iReply-shortcut.md)。

> 依赖通知带 RemoteInput reply action（短信/微信/QQ/Telegram 多支持）；验证码等无需回复的通知不挂回复按钮。公共 ntfy.sh 上 reply topic 明文，建议自建 ntfy + token。

---

## 五、使用建议

- **只想收验证码**：进入「过滤」页，开启「验证码自动提取」和「广告过滤」；再到「应用」页切到白名单模式，只勾选短信类 App。
- **想同步聊天**：保持黑名单模式（默认），在「过滤」页开启「微信 / QQ / Telegram 优化」。
- **通知没推过来**：先看「日志」页，每条通知（无论转发、过滤还是失败）都会记录原因。
- **想让通知带图标**：见下方「应用图标」一节。
- **电话通知不工作**：MIUI 不向第三方监听器分发系统电话通知，GotMsg 通过轮询 `getCallState()` 绕过此限制。需授予「电话」权限（设置 -> 应用 -> GotMsg -> 权限 -> 电话）。
- **断网收不到通知**：开启「设置 -> 短信兜底」并填好 iPhone 号码、授予短信权限。断网时验证码和来电走短信（消耗套餐额度，5 分钟限 1 条）。
- **想全平台通知**：可同时启用多个通道（勾选每个通道的多个条目），所有启用的会同时收到。

---

## 六、应用图标

Bark 和 ntfy 的通知 `icon` 字段需要公网可访问的图片 URL。GotMsg 支持把已安装 App 的图标批量导出，方便上传到你自己的图床。

规则：转发时 `icon = 图标 URL 前缀 + 安卓包名 + .png`。在「设置 -> 应用图标」里：

1. 填写图标 URL 前缀，例如 `https://你的图床域名/icons/`。
2. 选择一个目录，点「导出图标」，把该目录下所有 App 的图标以 `包名.png` 形式导出。
3. 把导出的图片上传到你的图床对应目录。

留空前缀则不显示图标。

---

## 七、界面截图

| 首页 | 应用管理 | 过滤设置 |
|---|---|---|
| ![首页](screenshots/home.png) | ![应用管理](screenshots/apps.png) | ![过滤设置](screenshots/filter.png) |

| 设置 | 转发日志 |
|---|---|
| ![设置](screenshots/settings.png) | ![转发日志](screenshots/log.png) |

---

## License

本项目仅供个人使用。自 v1.10.2 起闭源。

All Rights Reserved. 保留所有权利。
