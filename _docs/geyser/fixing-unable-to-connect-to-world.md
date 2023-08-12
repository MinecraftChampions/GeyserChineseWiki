---
title: 修复 '无法连接至世界'
---

无法连接至世界是许多人都遇到过的问题

# 在开始之前

## Java玩家也无法连接至世界

这个问题不会是Geyser造成的

## 我更新了Geyser之后就出现了此问题

重启试试

## 控制台有一堆报错!

请参阅 [常见异常](/geyser/common-issues/). 如果无法解决,请加入GeyserMC的 [Discord](https://discord.geysermc.org).

## 你被无限的重启困扰了吗

重启试试

# 是服务器的问题还是客户端的问题？

请分别将Java 版服务器 IP 以及基岩版的 IP 放在 https://mcsrvstat.us/ 网站查询.这是首先确定服务器是否是服务器问题的一种办法.

# 一般排除步骤

## 保证正确的ip

应该保证端口一致

## 我正在使用一个云主机 或者 VPS！

请阅读 [支持Geyser的 插件/服务商 列表](/geyser/supported-hosting-providers/).以查看您的托管或服务器提供商是否需要额外的配置步骤

## 端口转发

您的服务器需要进行端口转发.大多数情况下,您可以使用 Minecraft Java版的端口转发相关教程获取帮助；但是,您需要将其中的 TCP 替换为 UDP,并且默认情况下,将端口 25565 替换为 19132.

## 在 DNS 选项/端口转发中使用 TCP 而不是 UDP

请确保端口协议为`UDP`或`TCP/UDP`

## 端口小于10000

尽量不要把基岩版的端口设置成小于10000的值

## 基岩版玩家只能在服务器有人时加入

这可能时防火墙的问题,请尝试以下方法:

尝试通过网络浏览器连接到 Bedrock 的 IP 地址和端口,例如: `http://test.geysermc.org:19132`. 浏览器肯定不会反应,但再尝试进入有可能就成功了

特定服务器的修复:

SoYouStart (OVH子公司):

在控制面板中:
1. 点击ip选项卡
2. 点击那个齿轮,选择"Game mitigation".
3. 选择 "Add a rule".
4. 选择 "minecraftPocketEdition"然后输入udp端口
5. 保存并等待生效

## Issues connecting with OVH or a subsidiary

If you're running into issues with some Bedrock players being unable to connect on OVH, navigate through the following settings:

- Navigate to `Network interfaces` 
- Click on the `...` button on the table for your IP -> then `...` and `Configure the GAME firewall` -> `Add rule` -> `Other protocol` (or `minecraftPocketEdition` if available)
- Add your Geyser port into `outgoing port`

## 更改配置文件 'bedrock' 项的 'address'

更改配置文件 'bedrock' 项的 'address'

# 对于使用一些服务商的服主

## 翼龙面板

如果您在使用翼龙面板时遇到此错误,请尝试编辑 Geyser 配置并将端口更改为除“19132"之外的其他值（例如“25566"）.

## 在同一网络上的另一台计算机上使用 Geyser

### 只能在主机上连接,不能以其他任何方式连接

关闭防火墙

# 作为故障排除的最后手段...

下载 [MC基岩版服务端](https://www.minecraft.net/download/server/bedrock) 运行连接判断问题出在哪里

# Using Geyser on the same computer

## Windows 10/11

这只会影响尝试从 Windows 10 版加入 Geyser 且与 Geyser 服务器在同一台电脑上的人.
这是由未解除环回限制(Loopback restrictions)引起的问题. 默认情况下,微软应用对其所有本地连接的应用程序都有此限制. Geyser 将尝试自动解决此问题；但是,如果您在使用 Geyser 时若仍然遇到连接问题,您可以通过在管理员模式下在 Windows PowerShell 中输入以下内容来解除它:（如果正常执行,它应该返回“OK."）
```powershell
CheckNetIsolation LoopbackExempt -a -n="Microsoft.MinecraftUWP_8wekyb3d8bbwe"
```

如果这不起作用,您可以尝试以下步骤:
1. 按住Win+R
2. 输入 `hdwwiz.exe`, 回车
3. 手动安装硬件
4. 选择 网络适配器 > 下一步 > 左边选择 "Microsoft" > 右边选择 "Microsoft KM-TEST 环回适配器" 然后点击 下一步 直到完成.