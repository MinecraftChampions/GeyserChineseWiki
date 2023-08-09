---
title: 常见异常
---

# 已知异常和注意事项
如果你遇到的异常没有被收录,请加入Geyser 的 [Discord](http://discord.geysermc.org/).

## 运行命令异常

在某些情况时,你将 `username-prefix` 设置为了 带有`*`的字符串, 在输入命令时如果需要用到基岩版玩家名字, 你应该用引号包括; 如: `/tp "*qscbm187531"`. 设置为别的前缀可以解决这个问题.

## 如果你想使用IP转发, 请在 BungeeCord的 Floodgate 配置文件设置好!

如果你代理端的配置文件已经启动 `send-floodgate-data`,那么可能是子服没有安装Floodgate,或者是`key.pem`文件不同

## `java.lang.IllegalStateException: Cannot reply to EncryptionRequestPacket without profile and access token.`

请确保服务器已经安装并启动了Floodgate,否则请查看下一行的内容

## `javax.crypto.AEADBadTagException: Tag mismatch!`

如果同时在一台服务器安装了Geyser和Floodgate, 请删除 `floodgate` 文件夹, 并删除Geyser文件夹下的`key.pem`.
如果在不同的服务器, this could also be an error related to uploading through FTP. Using ASCII will not work here, and you need to make sure you're on binary when uploading. We recommend using [WinSCP](https://winscp.net/eng/index.php) if you need to use FTP.

## java.lang.NumberFormatException: For input string: ""

You're trying to log in without an Xbox account. Floodgate requires an Xbox account to authenticate the Bedrock player.

## Geyser-Floodgate:51777 lost connection: Internal Exception: java.lang.NumberFormatException: For input string: "SfqdXv36" (or a similar error)

Set `ip-forwarding` in your BungeeCord to `true`.

## "Please connect through the official Geyser" disconnect message

Ensure that Floodgate and Geyser are both up-to-date.

## Prefix is not changing on the server after changing it in the config.

Between the Paper builds of 1.15.2-355 and 1.16.5-505, there was a bug where Floodgate players who had already connected to the server would not have their prefixed changed. Paper builds 1.16.5-506 and later fix this issue.

Ensure that you removed the `usercache.json` file from the server root directory and restart your server.

## Issues with LuckPerms and prefixes

Set `allow-invalid-usernames` to `true` in LuckPerms' config.

## Failed to verify username! (with Paper)

To completely mitigate this issue, disable `perform-username-validation` in the [unsupported settings of the `config/paper-global.yml` file](https://paper.readthedocs.io/en/latest/server/configuration.html#unsupported-settings) (`paper.yml` in the root server folder on servers below 1.19). Using Floodgate on the backend servers will also mitigate this issue.

## Error with Forge or Fabric Bukkit Hybrid

At this time, there is no way to run Floodgate on servers that mix Forge and Bukkit or Fabric and Bukkit (For example: Magma, Mohist, and Cardboard/Bukkit4Fabric) - most hybrids do not support the complicated procedures we need to do in order to allow Bedrock players to connect (for the technically minded: these server softwares typically don't support NMS). 

If you wish to use Floodgate in combination with hybrid servers, we recommend putting these servers behind a BungeeCord or Velocity proxy, and running Floodgate on the proxy.
