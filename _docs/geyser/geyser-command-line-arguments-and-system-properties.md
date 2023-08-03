---
title: Geyser命令行参数
---

# Geyser命令行参数
Geyser提供了一些命令参数让你可以不修改配置文件修改配置或禁用一些控制台信息

### 配置属性
你可以通过以下命令参数为Geyser设置自动绑定的端口和ip
这主要用于服务商托管自动为Geyser进行设置

<div class="alert alert-info" role="alert">
    注意: 命令行参数优于配置文件
</div>

- ```-DgeyserUdpPort=server``` 或 ```-DpluginUdpPort=server```
  - ```-1``` 表示不支持UDP,自动禁用Geyser
  - ```server``` 表示匹配 Java 服务器一样的端口.
  - 其他的数字代表设置的端口

- ```-DgeyserUdpAddress=server``` 或 ```-DpluginUdpAddress=server```
  - ```server``` 表示匹配 Java 服务器一样的ip
  - 其他的字符串代表设置的ip

### 禁用警告和一些高级设置
您可以使用以下命令行参数禁用一些会打印到控制台的警告：

<div class="alert alert-danger" role="alert">
    警告: 禁用这些警告无法起到解决问题的作用
</div>

- ```-DGeyser.PrintSecureChatInformation=true```
  - 允许您禁用有关禁用安全聊天的警告. 因为这个警告是在服务器发送警告时发送的,因此此选项不再执行太多操作
- ```-DGeyser.ShowScoreboardLogs=true```
  - 允许您禁用与记分板相关的警告
- ```-DGeyser.ShowResourcePackLengthWarning=true```
  - 允许你禁用资源包路径过长的警告
- ```-DGeyser.PrintPingsInDebugMode=true```
  - 控制是否在调试模式下记录 ping 记录
- ```-DGeyser.UseDirectAdapters=true```
  - 允许您禁用 NMS 适配器的使用.禁用会导致性能受到损失,并且只能在调试模式下使用,另外此选项只能在Spigot系服务端使用
- ```-DGeyser.BedrockNetworkThreads=8```
  - 设置用于Geyser网络通信的线程数,建议不要设置

## Geyser独立版命令行参数:

#### `--config [文件路径]`
- **别名: `-c`**
- 指定一个路径下的 config.yml 文件使用.

#### `--gui` / `--nogui`
- **别名: `gui` / `nogui`**:
- 强制使用图形化页面启动/强制不使用图形化页面启动.

### 覆盖特定配置选项
通过覆盖特定配置选项,Geyser 直接优先读取参数内的配置,无视 `config.yml` 内对应的配置.

重写一个标准配置选项 (例如 `command-suggestions`):

`--command-suggestions=false`

重写一个嵌套配置选项(例如 `remote` 下的 `address`):

`--remote.address=test.geysermc.org`
