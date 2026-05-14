Ultra Fusion Remote WebUI V3.3.1 Pages 部署包

文件说明：
- index.html：远程 WebUI 主页面，部署到 GitHub Pages / 服务器时使用这个文件名。
- 这是纯静态页面，不需要后端服务器。
- 页面不要写死密钥；打开页面后在“连接设置”里填写，保存到当前浏览器本地 localStorage。

部署方式：
1. 新建一个 GitHub 仓库，例如 ultra-fusion-remote-webui
2. 上传 index.html 到仓库根目录
3. Settings -> Pages
4. Source 选择 Deploy from a branch
5. Branch 选择 main / root
6. 保存后等待生成访问地址

远程使用条件：
- 手机/电脑浏览器必须联网
- 家里的 ESP32-S3 中控也必须联网并连接巴法云 MQTT
- 主题保持 smarthomecmd / smarthomestatus / smarthomelog
2026年5月11日22：09，更新Ultra Fusion Remote WebUI V3.4 
2026年5月11日22：09，更新Ultra Fusion Remote WebUI V3.4.2
2026年5月14日14:   28,   更新灵汐V0.5体验版
