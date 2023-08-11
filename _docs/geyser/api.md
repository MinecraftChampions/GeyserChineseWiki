---
title: Geyser API
---

跟其他Java项目一样,Geyser也有属于自己的Api

### 我可以在哪里使用 Geyser API?
- 当你使用 Paper/Spigot, Velocity, Waterfall/BungeeCord等时,你可以在插件中引用GeyserApi
- 当你使用 Fabric 或者 Forge,你可以在mod中引用GeyserApi
- Geyser扩展

### 如何使用 Geyser API
看 [这里](/geyser/getting-started-with-the-api) 学会如何在你的项目中添加依赖

### 文档

GeyserApi提供了它的事件列表和一些api接口
如果你想学会如何编写Geyser扩展, 详见 [这里](/geyser/extensions).

**概述:** <br>
<div class="alert alert-info" role="alert">
    注意: 阅读 <a href="https://repo.opencollab.dev/javadoc/maven-snapshots/org/geysermc/geyser/api/2.1.2-SNAPSHOT">javadocs</a> 获取最好的体验.
</div>

#### [GeyserApi](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/GeyserApi.java):
GeyserApi接口充当了访问Geyser Api的入口
扩展至 [Base API](https://github.com/GeyserMC/api/blob/master/base/src/main/java/org/geysermc/api/GeyserApiBase.java) 接口.

GeyserApi类是Geyser API 的基类, 要使用Api必须访问它.<br>
要想访问,可以调用:
```java
GeyserApi.api();
```

在你获取接口实例之后你可以调用所有方法.<br>
大多数 [API 方法都有解释](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/GeyserApi.java).
由于GeyserApi扩展至Base Api, 你也可以使用 [Base API的方法](https://github.com/GeyserMC/api/blob/master/base/src/main/java/org/geysermc/api/GeyserApiBase.java).


#### 这边重点介绍一些方法:
`GeyserApi#isBedrockPlayer(UUID)`<br>
传入 **在线** 玩家的UUID 判断是否为基岩版玩家

`GeyserApi#connectionByUuid(UUID)`<br>
获取**在线**的基岩版玩家的 [Connection实例](https://github.com/GeyserMC/api/blob/master/base/src/main/java/org/geysermc/api/connection/Connection.java)<br>
如果传入的参数不是基岩版玩家的UUID,将会返回null

<div class="alert alert-info" role="alert">
    以上两个方法可以在登录前的的事件就调用
</div>

`GeyserApi#sendForm(UUID, Form(Builder))`<br>
发送表单给基岩版玩家.<br>
详见 [表单](/floodgate/forms/).

`GeyserApi#onlineConnectionsCount()`<br>
获取在线基岩版玩家的数量

### Geyser API的简要概述

#### [Cumulus](https://github.com/GeyserMC/Cumulus/tree/master/src/main/java/org/geysermc/cumulus) 
允许你向基岩版玩家发送表单,详见 [Cumulus](/geyser/forms/) 

#### [Events](https://github.com/GeyserMC/Geyser/tree/master/api/src/main/java/org/geysermc/geyser/api/event)
包含了所有Geyser触发的事件. 详见 [事件列表](/geyser/events) .

#### [Command](https://github.com/GeyserMC/Geyser/tree/master/api/src/main/java/org/geysermc/geyser/api/command)
包含了Geyser的命令相关类与接口, 使用 [Geyser 扩展](/geyser/extensions) 可以注册命令.

#### [Entity](https://github.com/GeyserMC/Geyser/tree/master/api/src/main/java/org/geysermc/geyser/api/entity)
代表了Geyser与实体相关的类与接口

#### [Item](https://github.com/GeyserMC/Geyser/tree/master/api/src/main/java/org/geysermc/geyser/api/item)
允许添加自定义物品,详见 [自定义物品](/geyser/custom-items) .

#### [Network](https://github.com/GeyserMC/Geyser/tree/master/api/src/main/java/org/geysermc/geyser/api/network)
包含通过[RemoteServer接口](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/network/RemoteServer.java)
获取的服务器信息,以及服务器协议版本等.
你可以通过[BedrockListener接口](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/network/BedrockListener.java)
获取Geyser监听的ip端口等

#### [Pack](https://github.com/GeyserMC/Geyser/tree/master/api/src/main/java/org/geysermc/geyser/api/pack)
包含了资源包的相关类和接口. 你可以创建自定义资源包.监听 [SessionLoadResourcePacksEvent](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/event/bedrock/SessionLoadResourcePacksEvent.java) 将资源包发送给连接的会话.
如果你想将资源包转发给所有连接的会话, 监听 [GeyserLoadResourcePacksEvent](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/event/lifecycle/GeyserLoadResourcePacksEvent.java).

通过 [PackCodec](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/pack/PackCodec.java), such as the provided [PathPackCodec](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/pack/PathPackCodec.java)
加载指定路径的资源包
```java
ResourcePack pack = ResourcePack.create(PackCodec.path(path));
```

#### [Extension](https://github.com/GeyserMC/Geyser/tree/master/api/src/main/java/org/geysermc/geyser/api/extension)
提供了有关扩展的相关类和接口.
详见 [Geyser扩展](/geyser/extensions).