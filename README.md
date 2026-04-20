# Totally Not Spyware

本项目是针对iOS 10.3.3 (arm64)设备专门编译的网页越狱分发包。可以部署在Nginx、Caddy和Apache等上面

## 🚀 以Nginx为例部署与运行

### 1. 获取资源
- 从 [Releases](../../releases) 下载最新的 `TNS.7z`。
- 解压到 Linux 服务器的 Web 目录（例如 `/var/www/tns`）。

### 2. Nginx 关键配置 (必须包含二进制下载声明)
编辑/etc/nginx/sites-enabled/default
```nginx
server {
    listen 80;
    server_name _; 
    root /var/www/tns;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }

    # 核心配置：将 payload 和 xz 压缩包作为二进制流分发
    location ~* ^/(payload|bootstrap/.*\.xz)$ {
        default_type application/octet-stream;
        add_header Content-Disposition "attachment";
    }
}
然后运行nginx -t&&nginx -s reload
3. 设备操作
进入“设置 -> Safari -> 清除历史记录与网站数据”。
在 Safari 访问 http或者https://<服务器IP>：<端口>。
```
### Credits

- The final ~~countdown~~ product: [Jake Blair](https://twitter.com/JakeBlair420)
- The entire frontend, website, etc.: [FoxletFox](https://twitter.com/FoxletFox)
- WebKit exploit: [Niklas Baumstark](https://twitter.com/_niklasb/), with part of [Samuel Groß](https://twitter.com/5aelo/)' code patched in.
- Everyone credited for the [DoubleH3lix](https://github.com/Siguza/doubleH3lix) and [Meridian](https://github.com/PsychoTea/MeridianJB) jailbreaks.
