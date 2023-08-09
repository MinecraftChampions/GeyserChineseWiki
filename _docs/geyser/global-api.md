---
title: 全局API
---

### 全局API
全局API可以在所有服务器上使用,它有如下功能: [全局连接](/floodgate/linking/#what-is-global-linking), [皮肤上传](/floodgate/features/#what-is-skin-uploading), 通过名称获取xuid, 通过xuid获取名称.
全局API不会存储任何其他数据. 全局API源代码在 [这里](https://github.com/GeyserMC/global_api), 全局连接服务器在 [这](https://github.com/GeyserMC/GlobalLinkServer).

作为使用全局API的用户, 你可以通过它获取任何一个有Geyser插件的服务器的基岩版玩家信息, 例如:
- 通过名称获取xuid, 通过xuid获取名称, 当然这里的信息只有缓存时才能获取. <br>
  当然, 你可以使用第三方API, 如 https://mcprofile.io/endpoints.
- 皮肤信息: 每当基岩版玩家进入一个有Floodgate的服务器时,他的皮肤信息就上传到了mineskin, 可以通过xuid获取资源版玩家的皮肤的base64值.

详见 [全局API文档](https://api.geysermc.org/docs).

### 示例
这里有一些示例能帮助你学会如何使用全局API. <br>

[GeyserDiscordBot](https://github.com/GeyserMC/GeyserDiscordBot/blob/master/src/main/java/org/geysermc/discordbot/commands/FloodgateUuidCommand.java) 
- 通过玩家名获取Floodgate玩家的uuid.<br>

[FabricGeyserPlayerHeads](https://github.com/onebeastchris/customplayerheads/blob/master/src/main/java/net/onebeastofchris/customplayerheads/utils/PlayerUtils.java#L54-L72)
- 通过全局API获取玩家皮肤, 并生成玩家头颅.