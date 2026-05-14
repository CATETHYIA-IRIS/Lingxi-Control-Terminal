灵汐体验版 V_0_5_0 Remote WebUI Pages 部署包

文件说明：
- index.html：GitHub Pages / 静态服务器使用的远程 WebUI 主页面，部署时保持文件名为 index.html。
- README.txt：当前部署说明文件。
- 本页面为纯静态 HTML 页面，不需要后端服务器。
- GitHub 版 WebUI 与灵汐体验版 V_0_5_0 本地 WebUI 保持整体风格一致，但不包含“智慧语音”页面。
- 智慧语音、ASR、TTS、按住说话、ConfirmAgent 语音授权等能力保留在 ESP32 中控本地 WebUI 中运行。
- GitHub 版主要用于远程设备控制、状态展示、系统日志、版本展示、论文截图和项目展示。

版本定位：
- 当前版本：灵汐体验版 V_0_5_0 Release Candidate
- 阶段定位：V_0 阶段毕业演示封版候选
- 核心能力：WebUI 主控、设备控制、状态展示、系统日志、天气/环境信息、三板架构展示、V_0.5 风格同步
- 本地完整能力：ESP32 中控 WebUI 保留智慧语音、录音文件识别、AI 回复、TTS 播放、问答式授权 Agent

安全说明：
- 页面不要写死任何真实密钥。
- 不要上传 WiFi 密码、API Key、Access Token、Secret Key、巴法云私钥、火山引擎/豆包密钥等敏感信息。
- 打开页面后，在“连接设置”中填写 MQTT 相关参数。
- 配置只保存到当前浏览器 localStorage，不会写入 GitHub 仓库。

部署方式：
1. 新建或打开 GitHub 仓库，例如 lingxi-remote-webui。
2. 上传 index.html 到仓库根目录。
3. 可同时上传 README.txt 作为部署说明。
4. 进入 Settings -> Pages。
5. Source 选择 Deploy from a branch。
6. Branch 选择 main / root。
7. 保存后等待 GitHub Pages 生成访问地址。
8. 访问生成的 Pages 地址，进入“连接设置”填写 MQTT 参数后使用。

远程使用条件：
- 手机或电脑浏览器必须联网。
- 家里的 ESP32-S3 中控必须联网。
- ESP32-S3 中控需要正常连接巴法云 MQTT。
- 远程 WebUI 通过 MQTT 与中控通信，不直接访问 192.168.4.1。
- 推荐主题保持：
  - 命令主题：smarthomecmd
  - 状态主题：smarthomestatus
  - 日志主题：smarthomelog

本地 WebUI 与 GitHub WebUI 区别：
- ESP32 本地 WebUI：
  - 完整 V_0_5_0 功能
  - 包含智慧语音、ASR、TTS、按住说话、ConfirmAgent
  - 适合在局域网或中控热点环境下使用
- GitHub WebUI：
  - V_0_5_0 风格同步版
  - 去掉智慧语音页面
  - 适合远程控制、状态展示、论文截图、面试展示和项目主页

版本更新记录：
- 2026年5月11日 22:09：更新 Ultra Fusion Remote WebUI V3.4
- 2026年5月11日 22:09：更新 Ultra Fusion Remote WebUI V3.4.2
- 2026年5月14日 14:28：更新灵汐 V_0_5_0 体验版远程 WebUI
- 当前版本：灵汐体验版 V_0_5_0 Release Candidate，GitHub 版同步本地 V_0.5 风格并移除智慧语音页

备注：
- 本仓库建议作为“灵汐 Remote WebUI 展示版 / 远程控制台”使用。
- 完整源码、真实密钥和硬件私有配置不建议放入公开仓库。
- 若后续进入 V_3 安全配置化阶段，可进一步将 API、Key、MQTT、AI 平台参数统一迁移到 WebUI 配置区管理。
