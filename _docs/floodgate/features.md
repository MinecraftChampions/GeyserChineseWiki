---
title: 功能
---

## 白名单命令

Floodgate 2.0 有着一个白名单命令: `fwhitelist`, 用于将基岩版玩家添加到`whitelist.json`(白名单文件). 不需要输入基岩版玩家的前缀 .

示例:
`fwhitelist add Tim203`
`fwhitelist remove Tim203`

同时你也可以使用UUID `fwhitelist add 00000000-0000-0000-0009-01f64f65c7c3`

它需要的权限为 `floodgate.command.fwhitelist`.

## 什么是皮肤上传?
要想Java玩家看到基岩版玩家的皮肤,就得安装Floodgate
如果看不见,就等一下.

皮肤上传是 [全局Api的一部分](/geyser/global-api).它负责将基岩版玩家的皮肤转换为Java版玩家的皮肤并上传到Mojang的服务器

GeyserMC使用 MineSkin. MineSkin 是在社区的赞助之下运行的. 所以如果你想支持MineSkin,详见 [此页面](https://mineskin.org/account).

![Example skin upload](https://cdn.discordapp.com/attachments/613168850925649981/815969801763160104/unknown.png)
