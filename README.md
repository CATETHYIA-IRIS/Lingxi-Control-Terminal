# 灵汐远程 WebUI（GitHub Pages 版）

这是灵汐全屋智能控制中心的远程控制页面。它不是本地 `192.168.4.1` 中控页面，而是部署在 GitHub Pages 上，通过巴法云 MQTT WebSocket 与家里的灵汐中控通信。

## 使用方式

1. 将本目录中的 `index.html` 上传或替换到你的 GitHub Pages 仓库。
2. 打开 GitHub Pages 网址。
3. 在登录页填写巴法云：
   - AppID
   - SecretKey
   - 命令主题
   - 状态主题
   - 日志主题
4. 点击“登录并连接”。
5. 连接成功后即可查看状态、远程控制设备、触发场景、查看日志。

## 默认主题

如果你的中控固件没有改过主题，保持默认即可：

- 命令主题：`smarthomecmd`
- 状态主题：`smarthomestatus`
- 日志主题：`smarthomelog`

远程下发控制时，页面会向：

```text
smarthomecmd/set
```

发布控制命令。

## 安全说明

不要把真实 AppID / SecretKey 写死到 GitHub 代码里。  
本页面只提供输入框，用户输入后会保存到当前浏览器的 localStorage。

这适合个人项目、毕业设计、演示和开发者自用。若要商业化，应改成服务器账号体系，由后端保存密钥并向前端发放临时 token。

## 与本地 V7.3 WebUI 的区别

本地 WebUI：

- 地址：`http://192.168.4.1`
- 服务器：ESP32 中控
- 登录：本地管理员账号
- 通信：本地 HTTP API
- 功能：完整，包括系统设置、节点管理、SD 资源、语音链路等

远程 WebUI：

- 地址：GitHub Pages
- 服务器：静态网页
- 登录：巴法云 AppID / SecretKey
- 通信：MQTT WebSocket
- 功能：远程控制、状态查看、场景触发、日志查看

远程版不能直接使用本地 `/api/...` 接口，也不直接访问 `192.168.4.1`。
