
配置 websocket 客户端

我的服务器 ssh 密码是 6lkh.

```
ssh root@124.71.204.54
```

然后。

启动是：

```
root@hcss-ecs-99d5:/xp/www/nodejs_ow# node app.js

WebSocket server is running on port 39001, v 4

^C

root@hcss-ecs-99d5:/xp/www/nodejs_ow# node app.js

WebSocket server is running on port 8099, v 5

新用户连接喽，目前总数 1

新用户连接喽，目前总数 1

新用户连接喽，目前总数 2

新用户连接喽，目前总数 2

新用户连接喽，目前总数 2
```

反正过了好久才连上。

------
接着，绑定域名，并申请 SSL。

注意！！！ 严禁开启强制 SSL ！ 可能会出错。

然后，设置 nginx 代理。添加如下内容即可：

```
# WebSocket 反向代理
location /ws/ {
	proxy_pass http://127.0.0.1:8099;   # 你的 WebSocket 服务
	proxy_http_version 1.1;
	proxy_set_header Upgrade $http_upgrade;
	proxy_set_header Connection "Upgrade";
	proxy_set_header Host $host;
}
```

-----

设置常驻进程。

# 使用 PM2（专门为 Node 后台常驻设计）

安装：

`npm install -g pm2`

启动：

`pm2 start /xp/www/nodejs_ow/app.js --name ow`

Ctrl+C、SSH断开，**都不会停止**。

查看列表：

`pm2 ls`

日志：

`pm2 logs ow`

停止：

`pm2 stop ow`

👉 你已经开发 WebGL 项目，**强烈推荐 PM2**，可自动重启、监控、部署、多进程。