# WeChat Services — Hermes Agent 插件集

微信生态功能插件合集，作为 [Hermes Agent](https://hermes-agent.nousresearch.com) 的插件运行。

## 插件列表

| 插件 | 路径 | 说明 |
|------|------|------|
| WeChat UOS Platform | `plugins/platforms/wechat_uos/` | 个人微信适配器 (itchat-uos 协议)，含群授权/盘搜/TG转发/CFTC上传/LSPosed模块更新 |

## WeChat UOS Platform

基于 itchat-uos（逆向 UOS 微信协议）的个人微信网关适配器。

### 功能

- **微信登录** — QR 码扫码，热重载
- **群 @ 消息响应** — 三级授权体系
- **盘搜** — 搜索夸克/115/百度/UC 网盘资源
- **TG 转发** — Telegram 频道→微信群自动转发
- **CFTC 上传** — 图片/文件上传到 CFTC 图床
- **LSPosed 模块更新追踪** — 监控 Xposed 模块更新并推送微信群
- **撤回消息缓存** — 群消息防撤回通知
- **GID 自动迁移** — itchat 重连后群 ID 变化自动处理

### 安装

在 Hermes Agent 配置中启用此插件：

```yaml
# config.yaml
plugins:
  - platform: wechat_uos
    enabled: true

env:
  WECHAT_UOS_ENABLED: true
```

或者克隆到 plugins 目录：

```bash
git clone https://github.com/gdjbdg5467/wechat-services.git \
  ~/.hermes/hermes-agent/plugins/platforms/wechat_uos
```

### 环境变量

| 变量 | 说明 |
|------|------|
| `WECHAT_UOS_ENABLED` | 启用插件 (true/false) |
| `WECHAT_UOS_ALLOWED_GROUPS` | 允许的群组 ID/名称，逗号分隔 |
| `WECHAT_UOS_ALLOWED_USERS` | 允许的用户昵称，逗号分隔 |
| `WECHAT_UOS_RESPOND_TO_DMS` | 是否响应私聊 |
| `WECHAT_UOS_QR_HTTP` | 是否启动 QR HTTP 服务 |
| `WECHAT_UOS_QR_PORT` | QR HTTP 端口 (默认 8646) |
| `WECHAT_UOS_HOME_CHANNEL` | 默认通知群组 |

### 群聊命令

发送 `@机器人` + 命令：

- `开启授权` / `关闭授权` — 群授权管理
- `授权 昵称` / `取消授权 昵称` — 成员权限管理
- `权限列表` / `刷新成员` — 查看/刷新权限
- `搜索 <关键词>` — 盘搜资源
- `开启盘搜` / `关闭盘搜` — 盘搜开关
- `开启转发` / `关闭转发` — TG转发开关
- `开启上传` / `关闭上传` — 图床上传开关
- `开启更新` / `关闭更新` — 模块更新推送开关
- `上传` — 上传最新媒体到图床
- `帮助` — 显示帮助