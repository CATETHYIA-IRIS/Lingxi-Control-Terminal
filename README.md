# 灵汐 Remote WebUI V6.0.5

这是灵汐系统的 GitHub Pages 远程控制台，用于外网查看状态、远程控制设备、切换场景和查看日志。

它不是 ESP32 本地 WebUI 的完整替代版。智慧语音、ASR、TTS、本机扬声器、SD 角色资源、角色头像/立绘、工程化诊断接口等能力仍然保留在 ESP32 中控本地 WebUI 中。

## 1. 文件说明

```text
index.html   GitHub Pages / 静态服务器入口页面
README.md    部署说明与安全说明
```

本页面是纯静态 HTML，不需要后端服务器，也不需要 Node.js、PHP、Python 服务。

## 2. 新版交互方式

新版页面采用“先连接，后进入控制台”的结构：

```text
打开 GitHub Pages
↓
进入灵汐 Remote 登录 / 连接页
↓
填写巴法云 MQTT WebSocket 参数
↓
点击“连接灵汐中控”
↓
MQTT 连接成功后进入远程控制台
```

如果只是展示页面，也可以点击“离线预览”。离线预览不会向家中设备下发任何控制命令。

## 3. 远程通信方式

远程 WebUI 不直接访问本地中控地址，例如：

```text
192.168.4.1
192.168.x.x
```

远程链路为：

```text
浏览器 / GitHub Pages
↓
巴法云 MQTT WebSocket
↓
家中 ESP32-S3 中控
↓
感知层 / 执行层节点
```

## 4. 推荐主题

默认主题保持和中控一致：

```text
命令主题：smarthomecmd
状态主题：smarthomestatus
日志主题：smarthomelog
```

实际下发控制时，页面会向：

```text
smarthomecmd/set
```

发布简单命令字符串，例如：

```text
light_living_on
light_living_off
light_bed_on
light_bed_off
relay_air
relay_tv
relay_fridge
relay_water_heater
window_toggle
scene_home
scene_away
scene_sleep
scene_movie
scene_office
scene_comfort
scene_night
scene_alarm
cloud_report
```

## 5. 连接参数说明

页面支持两种认证模式：

### 推荐：AppID / SecretKey

正式远程使用建议选择：

```text
认证模式：推荐：AppID / SecretKey
Host：bemfa.com
端口：9504
Path：/wss
AppID：填写自己的 AppID
SecretKey：填写自己的 SecretKey
```

### 测试：私钥作为 ClientID

调试时可以选择：

```text
认证模式：测试：私钥作为 ClientID
私钥 UID：填写巴法云私钥
```

但测试模式存在风险：如果浏览器和 ESP32 中控使用同一个私钥作为 ClientID，可能会互相挤下线。因此正式远程建议使用 AppID / SecretKey。

## 6. 安全说明

请务必注意：

```text
不要把真实 WiFi 密码上传到 GitHub
不要把真实巴法云私钥上传到 GitHub
不要把真实 AppID / SecretKey 写死进 index.html
不要上传火山引擎、豆包、ASR、TTS、天气等平台密钥
```

页面中的配置只保存在当前浏览器的 localStorage 中，不会写入 GitHub 仓库。

如果你勾选“记住配置到本机浏览器”，浏览器会在本机保存 MQTT 参数。公共电脑或借用电脑不建议勾选。

## 7. 与 ESP32 本地 WebUI 的区别

### ESP32 本地 WebUI

适合在局域网或中控热点下使用，功能完整：

```text
完整首页
设备管理
系统设置
SD 角色资源
头像 / 立绘
智慧语音
中控录音
ASR
TTS
本机扬声器播报
WebUI 重播
规则引擎
工程化诊断接口
```

### GitHub Remote WebUI

适合公网远程控制和项目展示，功能轻量：

```text
连接 / 登录页
首页总览
环境状态
设备控制
智慧生活场景
系统日志
连接设置
项目说明
```

远程页面不读取 SD 卡，因此不会显示角色头像、立绘、SD 语音包，也不会提供本机录音、ASR、TTS、扬声器播放等本地能力。

## 8. 部署到 GitHub Pages

1. 打开你的远程 WebUI 仓库。
2. 替换仓库根目录的 `index.html`。
3. 替换仓库根目录的 `README.md`。
4. 提交并推送：

```bash
git add index.html README.md
git commit -m "Update Lingxi Remote WebUI V6.0.5"
git push
```

5. 打开 GitHub 仓库的 Settings。
6. 进入 Pages。
7. Source 选择 Deploy from a branch。
8. Branch 选择 main / root。
9. 等待 GitHub Pages 部署完成。
10. 打开生成的 Pages 地址。

## 9. 使用前检查

远程控制要正常工作，需要满足：

```text
手机或电脑浏览器可以联网
家中的 ESP32-S3 中控可以联网
中控已经成功连接巴法云 MQTT
中控使用的主题与 Remote WebUI 页面填写的主题一致
浏览器填写的巴法云认证参数正确
```

## 10. 故障排查

### MQTT 显示未连接

检查：

```text
Host 是否为 bemfa.com
端口是否为 9504
Path 是否为 /wss
认证模式是否选对
AppID / SecretKey 或 UID 是否填写正确
浏览器网络是否允许 wss 连接
```

### MQTT 已连接但中控未知

可能原因：

```text
中控没有联网
中控没有连接巴法云 MQTT
状态主题不一致
中控没有上报 smarthomestatus
```

可以点击：

```text
请求上报
```

页面会向命令主题发送：

```text
cloud_report
```

### 点击设备没有反应

检查：

```text
命令主题是否正确
中控是否在线
执行层节点是否在线
中控固件是否支持对应命令
```

### 页面显示离线预览

离线预览只用于展示 UI，不会真的控制设备。

## 11. 版本定位

```text
远程页面版本：灵汐 Remote WebUI V6.0.5
配套中控版本：Lingxi_V6_0_5_ArduinoTabsModular_REAL_PATCHED
感知层建议版本：Lingxi_SensorNode_V3
执行层建议版本：Lingxi_ActionNode_V3
```

本版本用于配套 V6.0.5 工程化封版版本。远程端保持轻量，本地端保持完整。

## 12. 后续扩展方向

后续可以继续扩展：

```text
远程账号登录
二维码绑定中控
多家庭 / 多网关切换
状态 JSON 协议版本号
设备模板远程同步
告警推送
历史曲线
移动端 PWA 安装
```

当前版本优先保证轻量、稳定和不泄露密钥。
