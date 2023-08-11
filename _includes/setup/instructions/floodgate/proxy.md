# Floodgate setup on a BungeeCord/Velocity proxy

<div class="alert alert-info" role="alert">
	你可以只在代理服务端上安装Floodgate, 但是建议在所有子服务器上安装Floodgate
</div>

1. 首先下载 [Floodgate](https://geysermc.org/download). 
2. 把文件丢到 `plugins` 目录, 然后重启服务器.
3. 设置Geyser配置文件中的 `auth-type` 为 `floodgate`.
4. 重启服务器

## 在子服务器搭建Floodgate

如果你想要在子服务器安装Floodgate,请继续阅读

1. 在代理端安装好Floodgate之后,在所有子服务器安装Floodgate
2. 如果你使用BungeeCord请启用`config.yml` 里的 `ip_forward`. 如果使用Velocity, 设置 [玩家信息转发](https://docs.papermc.io/velocity/player-information-forwarding).
3. 在`spigot.yml`启用bungeecord. 使用Velocity请参阅Velocity的文档
4. 启动服务器
5. 编辑 代理端的 Floodgate 配置文件 中的 `send-floodgate-data` 为 true.
6. 复制代理端的 `key.pem` 到所有子服务器
7. 重启服务器

<div class="alert alert-warning" role="alert">
	不要泄露`key.pem`,这是你服务器的密钥
</div>