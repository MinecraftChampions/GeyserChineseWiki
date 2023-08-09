# 在Geyser独立版设置Floodgate

<div class="alert alert-info" role="alert">
	请注意,本教程指在服务器安装Floodgate后,独立版配置
</div>

1. 下载 [Floodgate](https://geysermc.org/download).
2. 在服务器上安装 Floodgate
3. 更改配置文件的`auth-type`为`floodgate`
4. 把 服务器 Floodgate目录下的 `key.pem` 丢到Geyser独立版目录下
5. 启动Geyser独立版

<div class="alert alert-warning" role="alert">
	不要泄露`key.pem`,这是你服务器的密钥
</div>
