---
title: 常见异常
---

在很多时候,在使用 Geyser 时会遇到无法连接到服务器类似的错误,这个页面能够试着帮你解决这些异常,如果没有解决,请加入 [GeyserMC's Discord](https://discord.gg/geysermc) 寻求支持.

# Floodgate
有关Floodgate的异常请看: [这里](/floodgate/issues/).

# 无法正常连接到服务器! (服务器在好友选项卡没有显示或者在连接服务器时出现 "无法连接到世界")
* 如果你没有使用方向代理, 请保证 `enable-proxy-protocol` 的值为 false

## 如果服务器不在好友选项卡中

* *如果使用 Windows 10, iOS, or Android*: 把服务器添加到服务器列表.
* *如果使用 Xbox One*: 尝试使用 [BedrockConnect](/geyser/using-geyser-with-consoles/).
* *如果使用 PS4*: [尝试使用LAN连接.](/geyser/using-geyser-with-consoles/#playstation-4)
* *如果使用 Nintendo Switch*: 无法通过好友选项卡中的会话加入服务器, 请使用 [BedrockConnect](/geyser/using-geyser-with-consoles/).

*如果Geyser在本地:* 请尝试使用 `localhost` 或者 `0.0.0.0` 当作ip,通过服务器形式连接

## 点击 [这里](/geyser/fixing-unable-to-connect-to-world/) 来修复 "无法连接至世界" 并且没有控制台报错

### 启动时提示`java.net.BindException: Address already in use: bind`.
端口被占用了,如果找不到冲突的软件,可以尝试重启

### [...]` has been compiled by a more recent version of the Java Runtime (class file version 60.0)`

升级 Java 16: https://paper.readthedocs.io/en/latest/java-update/index.html.

### 您的服务商可能没有及时打开UDP端口

这一般意味着主机没有开放UDP端口,JAVA协议是TCP,Bedrock协议是UDP,可以尝试联系服务商

# 卡在 "正在连接服务器" 且后台没有报错

首先尝试重启客户端

然后尝试更新Java版本 [Adoptium.net](https://adoptium.net/).

可能为网络问题. 把 `mtu` 选项慢慢调低并尝试

# 登录失败

***如果你使用的是插件版本:*** 请检查你的配置文件确定监听的ip为 `127.0.0.1`.

### Cannot reply to EncryptionRequestPacket without profile and access token

两个可能的原因:

*Floodgate问题*:

如果您配置启用了 Floodgate 可能会出现此消息. 通常,这意味着您的 Floodgate 配置是错误的,或与其他插件冲突.如果您曾将 Floodgate 的密钥文件复制到 同一服务器 上的 Geyser 文件夹,那么 Geyser 文件夹内的密钥文件就是多余的.您可以放心的删除复制到 Geyser 文件夹中的密钥文件,重新启动服务器.
*服务器开了正版验证,Geyser配置离线模式*:

If you have your configuration set up like this, put simply, it won't work. If authentication for the Java server is set to online, it is expected Geyser is configured the same way. The server requires a valid Minecraft: Java Edition account, and if you aren't logging into one with Geyser, then you will be unable to join the server. If your configuration is set up properly and you're still getting this issue, it could be that your credentials are invalid.

### Connection Refused: <INSERT IP AND/OR DOMAIN>

连接被拒绝通常意味着请求该端口时无法连接 Java 服务器,或者服务器拒绝访问网络级别的外部连接.后者可能会发生在类似 TCPShield 等 DDOS 防护插件上,如果您没有类似的 DDOS 防护插件,请确保您尝试连接的服务器连接 IP 或域名在配置中拼写正确,已启动且端口转发正确.
如果您从旧版本的 Geyser 进行更新,请将您的远程地址设置为auto,然后重试.

### Floodgate Misconfiguration
查看这个 [页面](/floodgate/issues/) .

### Missing profile key. This server requires secure profiles.

查看这个 [页面](/geyser/secure-chat/).

### Mojang Resetting Account Credentials
Geyser独立版不会有此异常,请使用Floodgate插件,它允许基岩版客户端在不需要 Java 版帐户的情况下加入您的服务器.

# 基岩版客户端提示 "无效IP地址"
请尝试使用ipv4

# 基岩版客户端在使用指令时出现卡顿或者崩溃
这是一个老问题,Java的命令补全导致了卡顿,我们可以通过插件来设置补全的命令[CommandWhitelist](https://www.spigotmc.org/resources/81326/)
也可以通过禁用 `command-suggestions` 选项

# BungeeCord 在基岩版玩家加入后卡顿或者崩溃
请确保你的 BungeeCord 的 `config.yml` 配置文件中将 `ip-forward` 设置为 `true` 并在你的所有子服的 `spigot.yml` 配置文件中将 `bungeecord` 设置为 `true`.

# Failed to load locale asset cache: Unrecognized token 'Cannot'
增加命令行参数:`-Djava.net.preferIPv4Stack=true`,启动脚本内容就像`java -Xms1024M -Djava.net.preferIPv4Stack=true -jar Geyser.jar`一样·

# Outdated client! Please use 1.x.x
更新Geyser版本

# Outdated server! I'm still on 1.x.x

更新服务器版本,或者使用 [ViaVersion](https://viaversion.com/). 也可以使用 [VIAaaS](https://github.com/ViaVersion/VIAaaS) (ViaVersion as a Service).

# Query: Incorrect Magic!

参阅: https://www.spigotmc.org/threads/query-incorrect-magic-and-high-cpu-usage.159386/#post-2709057

* 当你不使用方向代理时保证 `enable-proxy-protocol` 的值为 false.

# 只在安装 Floodgate 的 BungeeCord 服务器上有效

请在所有子服上安装Floodgate

并且保证 `key.pem` 和 `config.yml` 在所有子服都是一样的

如果您的玩家无法从大厅连接到另一个子服,请检查控制台.
### 可能造成该问题的插件
* `HamsterAPI`
