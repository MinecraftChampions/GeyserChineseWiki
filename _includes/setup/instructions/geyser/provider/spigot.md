
# 在Spigot系服务端搭建Geyser

<div class="alert alert-info" role="alert">
    如果你的服务器的版本不是 {{ site.data.versions.java }}, 请使用 <a href="https://www.spigotmc.org/resources/viaversion.19254/">ViaVersion</a>.
    另请查看有关于Geyser支持版本的 <a href="/geyser/faq/#what-server-versions-does-geyser-support">常见问题页面</a>.
</div>

1. 选择你的服务器核心
2. 从 [下载页面中](https://download.geysermc.org/v2/projects/geyser/versions/latest/builds/latest/downloads/spigot) 下载Geyser.
3. 把Geyser放到`plugins`目录, 并重启服务器
4. 编辑位于 `/plugins/Geyser-spigot/config.yml` 的配置文件, 找到以下内容:

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
5. 可以通过在控制台运行 `geyser connectiontest <ip>:<port>` 命令检验是否生效

<div class="alert alert-info" role="alert">
   要允许基岩版不登录正版Java账号可以加入服务器的话可以使用 <a href="/floodgate/setup/">Floodgate</a>.
</div>
