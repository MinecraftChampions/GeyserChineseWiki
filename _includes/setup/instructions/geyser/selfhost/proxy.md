
# 在代理端上搭建Geyser(BungeeCord/Velocity)

<div class="alert alert-info" role="alert">
    注意: <br>
    - <b>只需要</b> 在代理端安装Geyser! 你可以在所有子服上安装Floodgate获取更好的皮肤体验以及 
        为其他插件提供Floodgate Api. <br>
    - 所有子服务器必须支持 {{ site.data.versions.java }} Java 客户端加入, 因为Geyser只模仿了一个客户端.  
</div>

1. 从 [下载页面中](https://geysermc.org/download) 下载Geyser.
2. 把Geyser放到`plugins`目录,最后重启服务器
3. 编辑位于 `/plugins/Geyser-xyz/config.yml` 的配置文件, 找到以下内容:

    ```yaml
    bedrock: 
        # Geyser开启的地址,正常情况下,不做修改
        #address: 0.0.0.0

        # Geyser转发的端口
        port: 19132

        # 服务器每次开启时,Geyser 所开启的端口和 Java版服务器是否保持一致.需要注意的是,Geyser独立版无法使用此选项
        clone-remote-port: false
    ``` 
   最重要的部分就是Geyser转发的端口这个设置,基岩版玩家将通过这个端口加入服务器
   部分服务商会要求修改部分设置,比如修改端口,如果需要的话还可以设置 clone-remote-port 和 address.
   启用了 `clone-remote-port`后,Geyser转发的端口会被替换为 Java 的端口！
   重要提示：其他依赖 UDP 端口的服务或插件（如语音聊天或查询功能）不能和 Geyser 共用同一个端口.

4. 连接至服务器
   <br> <br>
   **在局域网中连接** <br>
   在同一个设备中可以使用 `localhost`, 或者 `127.0.0.1` 作为域名加入
   如果出现问题,请访问 [修复无法连接至世界](/geyser/fixing-unable-to-connect-to-world/#Using-Geyser-on-the-same-computer).
   如果在同一局域网中不同设备你需要通过局域网ipv4进行连接 - 一般以 `10.` 或 `192.168.` 开头.
   <br> <br>
   **在公网中连接**<br>
   如果你想希望你的服务器可以让其他玩家加入
   你有两种方法可以选择: <br>

    - 开放端口(有公网ip): 一定要开放UDP端口,关闭防火墙,保证能联通

    - 内网穿透(无公网ip): 使用类似playit.gg的网站

5. 可以通过在控制台运行 `geyser connectiontest <ip>:<port>` 命令检验是否生效

<div class="alert alert-info" role="alert">
   要允许基岩版不登录正版Java账号可以加入服务器的话可以使用 <a href="/floodgate/setup/">Floodgate</a>.
</div>