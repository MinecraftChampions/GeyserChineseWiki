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
如果在不同的服务器, 可能是因为FTP上传的原因. 不要使用ASCII编码, 并且当成二进制文件上传. GeyserMC推荐使用 [WinSCP](https://winscp.net/eng/index.php) (译者本人也在使用).

## java.lang.NumberFormatException: For input string: ""

基岩版玩家没有Xbox账号进行登录时会触发

## Geyser-Floodgate:51777 lost connection: Internal Exception: java.lang.NumberFormatException: For input string: "SfqdXv36" (或者类似错误)

请把BungeeCord 的 `ip-forwarding` 改为 `true`.

## "Please connect through the official Geyser"

更新Geyser和Floodgate

## 更改基岩版前缀后不生效

在paper的 1.15.2-355 和 1.16.5-505 版本会触发, 更新paper版本解决

另外请确保删除服务端根目录下 `usercache.json` 文件后重启服务端

## LuckPerms前缀相关问题

在LuckPerms配置文件里启用 `allow-invalid-usernames`

## Failed to verify username! (无法验证用户名,Paper)

要想解决此问题, 在 [`config/paper-global.yml`文件](https://paper.readthedocs.io/en/latest/server/configuration.html#unsupported_settings)禁用 `perform-username-validation`  (在低于1.19的paper服务器中`paper.yml`在服务器根目录). 在代理服务器上使用Floodgate可以解决此问题.

## 在模组插件混合端中使用Floodgate报错

目前,Floodgate还不支持在混合端上运行.

想要使用Floodgate, 请把Floodgate丢到代理服务端
