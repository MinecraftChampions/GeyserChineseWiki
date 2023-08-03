# 搭建Geyser独立版

<div class="alert alert-info" role="alert">
   你需要Java16及更高版本才能使用. 如果你想在Android设备或者IOS设备使用,请下滑到底部
</div>

1. 从 [下载页面中](https://download.geysermc.org/v2/projects/geyser/versions/latest/builds/latest/downloads/standalone) 下载Geyser
2. 新建一个目录,并把Geyser丢进去
3. 启动Geyser:
   - **GUI页面** (推荐): <br>
   双击Geyser文件
   - 使用 **控制台**: <br>
   使用启动脚本启动,具体请参阅[创建Geyser独立版启动脚本](/geyser/creating-a-startup-script/)  <br>

4. 打开Geyser设置文件 (`config.yml`), 并找到下面这段:

   ```yaml
   bedrock: 
      # Geyser开启的地址,正常情况下,不做修改
      #address: 0.0.0.0
   
      # Geyser转发的端口
      port: 19132
   ```
   `port`是基岩版进入服务器的端口
   当你要限制进入Geyser的ip才对`address`做出修改
   <br>

   需要设置Geyser进入哪个服务器,请继续修改
   ```yaml
   remote:
      # Geyser监听的ip地址
      # 当为"auto"时,默认为本机地址.
      address: auto

      # 监听的端口
      port: 25565
      
      # 登录方式,有offline,online,floodgate (详见 https://github.com/GeyserMC/Geyser/wiki/Floodgate).
      auth-type: online
   ```
   更改`address`设置Geyser监听的ip
   然后, 设置 `port` 为Java服务器的端口. 如果服务器上有Floodgate插件, 你可以设置 `auth-type` 为 "floodgate" - 如果没有, 
   当服务器有正版验证时设置为 `online`, 否则设置为 `offline` . 要安装Floodgate,详见 [搭建Floodgate](/floodgate/setup). <br>
   
5. 连接至服务器
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

6. 可以通过在控制台运行 `geyser connectiontest <ip>:<port>` 命令检验是否生效

# 运行Geyser在IOS/Android

<div class="alert alert-warning" role="alert">
      Android上的Termux等软件运行Geyser会在很大程度上受到设备性能的设置,请自行承担后果
</div>

## Termux (Android)
1. 下载并安装 [Termux](https://termux.com/)
2. 运行 `pkg install openjdk-17`
3. 运行 `wget https://ci.opencollab.dev/job/GeyserMC/job/Geyser/job/master/lastSuccessfulBuild/artifact/bootstrap/standalone/build/libs/Geyser-Standalone.jar`
4. 运行 `java -jar Geyser-Standalone.jar`

或者

Geyser有一个自动安装的脚本,运行以下命令以开始下载/安装
```
curl https://gist.githubusercontent.com/rtm516/e3e07d6595ee41e05a38b03c0f4d7a80/raw/install.sh | bash
```

## NewTerm 2 (iOS)
**注意:** 你需要事先进行越狱
1. 安装 [Filza File Manager](http://cydia.saurik.com/package/com.tigisoftware.filza/).
2. 安装 [NewTerm 2](https://chariz.com/get/newterm).
3. 下载 [这里](https://github.com/PojavLauncherTeam/PojavLauncher_iOS/releases/download/v16-openjdk/openjdk-16-jre_16.0.0+git20201217.8383f41-2_iphoneos-arm.deb) 的 jre16(IOS版).
4. 下载 [这里](https://cdn.discordapp.com/attachments/558829512633090048/834014323755319306/com.letschill.java_0.1_iphoneos-arm.deb) 的 修改后的 java 指令集 并通过 Filza 进行安装.
5. 打开 NewTerm 2 并运行 `wget https://download.geysermc.org/v2/projects/geyser/versions/latest/builds/latest/downloads/standalone`
6. 运行 `java -jar Geyser-Standalone.jar`.
7. 成功

**注意:**
在某些时候,IOS可能会杀死进程.如果遇到错误的话,可以运行 su 然后输入root密码(默认是 alpine)获得 root 权限.再开启Geyser,应该就能成功运行.