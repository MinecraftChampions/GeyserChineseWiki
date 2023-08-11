---
title: 常见问题
---

# 常见问题

## 改变/禁用 前缀

***请注意: 不建议禁用前缀,因为Java用户和基岩版用户难免会有重名.同理,如果你是离线服,也建议给离线玩家加上前缀***

在Floodgate配置文件中, 更改 `username-prefix` 为你想要的前缀 - 同时如果像禁用它,可以直接设置为 `""`

在老版本Paper服务端使用时,建议删除 `usercache.json` 文件,详见[此页](/floodgate/issues/#更改基岩版前缀后不生效) .

## 获取基岩版玩家的uuid
控制台日志玩家加入时有显示, 或者使用 [此页面](https://uuid.kejona.dev/). 如果没有效果,请尝试以下方法:

首先,你需要获取玩家的xuid. 有许多第三方网站可以做到这一点, 例如, [这一个](https://www.cxkes.me/xbox/xuid) (与GeyserMC无关). 选择 "Hexidecimal."(16进制) 然后输入玩家的Xbox名称(代号), 然后点击提交, 然后就会显示以下格式的xuid `xxxxxxxxxxxxxxxx`. 要想转换xuid为uuid, 请把uuid转换为以下格式 `00000000-0000-0000-xxxx-xxxxxxxxxxxx`. 如果格式正确,这就是uuid.

## 使用 变量 (PlaceholderAPI)
如果你使用Spigot版本的Floodgate, 可以下载 [此插件](https://github.com/rtm516/FloodgatePlaceholders/). 使用变量只需要安装 [PlaceholderAPI](https://www.spigotmc.org/resources/6245/),不需要做一些其他的设置. 如果在BungeeCord等代理服务端,详见搭建章节.

## 使用 Skript
在 [这里](https://github.com/Camotoy/floodgate-skript). 
