---
title: 绑定
---

## 绑定系统

什么是绑定系统,很好理解,就是将基岩版账号和Java版账号绑定起来,当服务器启用这个功能的时候,基岩版玩家进入时默认就会游玩它绑定的Java账户

注意:如果你绑定了Java帐号之后,进入服务器只会游玩Java的账号,所有数据都是你Java的账号,你将无法游玩你基岩版的账号.要想继续使用基岩版账号,可以取消绑定.


## 什么是全局绑定?
详见: [https://link.geysermc.org/](https://link.geysermc.org/)

在我们开发出全局绑定这个系统之前,大部分的服务器都是使用本地绑定,用户每加入一个服务器就要绑定一次,还给服务器添加了负担.在全局绑定出现之后,用户再也不需要繁琐的操作,
只需要一次绑定,随处可用(仅限于开启了这个功能的服务器)

全局绑定基于 [全局API](/geyser/global-api).

目前,想要绑定账号又两种方法:

#### 使用全局绑定服务器绑定你的账户:
如果你想绑定账户,教程如下:
1. 使用你的Java账户加入全局绑定服务器
(IP: `link.geysermc.org`, Java端口: `25565`, 基岩版端口: `19132`)
2. 进入之后使用 `/linkaccount` 命令
3. 输入命令之后输入命令的那个账号会收到验证码
4. 然后在不是输入命令的那个账号使用 `/linkaccount <code>` 命令
5. 然后你就会被提出服务器,并显示已经绑定成功的消息

要想取消绑定,请再次加入服务器并输入 `/unlinkaccount` 指令. 

#### 使用网页进行绑定:
  详见:https://link.geysermc.org/method/online

### 配置
默认情况下Floodgate 2.0 都启用了全局绑定,相关配置文件如下:
```yml
# 绑定系统配置项
player-link:
  # 是否启用
  enabled: true
  # 是否使用全局绑定
  use-global-linking: true
```
([更全的配置](https://github.com/GeyserMC/Floodgate/blob/master/core/src/main/resources/config.yml#L25-L59))

## 本地绑定
你可以自己搭建数据库存储绑定信息,本地绑定可以和全局绑定一起使用,优先级是本地绑定 > 全局绑定

如果你使用代理端,只需要在代理端操作

1. 下载 [数据库扩展](https://ci.opencollab.dev/job/GeyserMC/job/Floodgate/job/master/).
   如果你不知道什么是数据库的话,或者没有安装数据库,请使用`sqlite`.数据库扩展文件名为: `floodgate-*类型*-database.jar`.
2. 把文件丢到Floodgate目录下 (例如 `/plugins/floodgate/`).
3. 启用 `player-link` 中的 `enable-own-linking`.
4. 设置 `player-link` 中的 `type` 为你的数据库版本  (Floodgate 1.0 总是为 `sqlite`).
5. 重启服务器

如果你选择了 `mysql` 那Floodgate会生成一个文件让你配置相关信息

然后在服务器输入 `/linkaccount` 指令进行绑定 .
