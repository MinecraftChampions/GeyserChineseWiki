
# 搭建Floodgate-Fabric

1. 下载 [Floodgate](https://modrinth.com/mod/floodgate). 
2. 把 Floodgate-Fabric.jar 丢到 `mods` 文件夹, **注意需要 [FabricAPI](https://modrinth.com/mod/fabric-api) installed.**
3. 把Geyser配置文件里的 `auth-type` 改为 `floodgate`.
4. 重启服务器.


**如果使用Velocity请注意:**
你需要配置 FabricProxyLite 以启用Fabric服务器从Velocity接受数据