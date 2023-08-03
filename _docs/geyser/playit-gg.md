---
title: playit.gg 设置
---

<div class="alert alert-info" role="alert">
	本页面是配置内网穿透的,国内软件同理
</div>

## 先决条件

<div class="alert alert-info" role="alert">
   能够本地访问运行的Geyser服务器
</div>

- 如果你已经运行设置了playit.gg,那么可以跳过步骤1.2,直接学习步骤3

## Setup
1. 下载它并且注册登录
2. 登录后,请确保连接程序和网站,直到达到第4步为止.如果没有自动连接,请按照网站和playit.gg程序控制台上的指示进行操作.
   ![img](https://cdn.discordapp.com/attachments/613194762249437245/1101302643214794863/image.png)
3. 如果你看到上述界面,请点击"Create Tunnel",或者在登录到你的账户后选择"Tunnels"选项卡.然后选择"Minecraft Bedrock",勾选"Enable Tunnel",最后单击"Add tunnel"。
   ![img](https://cdn.discordapp.com/attachments/613194762249437245/1101305135768027156/image.png)
4. 单击"Add tunnel"之后, 会创建一个新的隧道, 然后就设置好了! 往下滑动界面, 你应该看到如下的界面:
   ![img](https://cdn.discordapp.com/attachments/613194762249437245/1101306419640270858/image.png)
   如果你的 Geyser 映射端口设置的不是19132请更改端口.如果你的服务器不部署在本地,请更改ip.
5. 设置完成，你应该得到类似的IP("180.ip.ply.gg:18213"),分号前面是域名,后面是端口.
6. 如果能够正常加入服务器,那么说明一切都已经设置好了,另外,请不要关闭playit.gg,如果关闭,内网穿透就不再生效
   (如果无法加入,请查看[故障排除](/geyser/setting-up-playit-gg/#troubleshooting).) 

## 异常排除

### 我无法连接至服务器
* *请优先检查控制台是否有报错和相关信息.*
* *然后查看 [修复无法连接世界](/geyser/fixing-unable-to-connect-to-world/).*
* *请回顾步骤5,查看Geyser设置端口和playit设置的端口是否一直.*
