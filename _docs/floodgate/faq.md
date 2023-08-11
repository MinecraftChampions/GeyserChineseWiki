---
title: 常见问题
---

# 常见问题

## 改变/禁用 前缀

***请注意: 不建议禁用前缀,因为Java用户和基岩版用户难免会有重名.同理,如果你是离线服,也建议给离线玩家加上前缀***

在Floodgate配置文件中, 更改 `username-prefix` 为你想要的前缀 - 同时如果像禁用它,可以直接设置为 `""`

在老版本Paper服务端使用时,建议删除 `usercache.json` 文件,详见[此页](/floodgate/issues/#更改基岩版前缀后不生效) .

## Obtaining UUIDs for Floodgate players
Check your server logs, or use [this](https://uuid.kejona.dev/) page. If this doesn't work, then try this method:

First, you'll need to get the XUID of the player. There are several third-party websites to find this, for example, [this one](https://www.cxkes.me/xbox/xuid) (unaffiliated with Geyser). Make sure to choose "Hexidecimal." You'll need to enter the player's Xbox Gamertag, and, once submitted, and it should display the XUID in the format of `xxxxxxxxxxxxxxxx`. To turn the XUID into a UUID that Java Edition can recognize, you need to put the XUID in this format: `00000000-0000-0000-xxxx-xxxxxxxxxxxx`. If formatted right, Java Edition should accept it as a UUID.

## Using PlaceholderAPI
If you're using the Spigot version of Floodgate, download the Placeholder plugin [here](https://github.com/rtm516/FloodgatePlaceholders/). Using the placeholders shouldn't require additional setup other than having [PlaceholderAPI](https://www.spigotmc.org/resources/6245/) installed. See the section above on installing Floodgate on backend servers if you wish to use this on BungeeCord.

## Using Skript
If you're using the Spigot version of Floodgate, there is an unofficial plugin that adds Skript support [here](https://github.com/Camotoy/floodgate-skript). 
