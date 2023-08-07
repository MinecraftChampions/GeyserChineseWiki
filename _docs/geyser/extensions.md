---
title: Geyser 扩展
---

## Geyser 扩展
Geyser 相当于 "plugins", 但是它不运行在服务端,是由Geyser运行,所以不必担心跨平台.  

### Geyser 扩展可以做什么?
Geyser扩展可以使用GeyserApi,详见 [Geyser API 文档](/geyser/api/),举几个例子:
- 注册自定义物品
- 隐藏命令补全
- 自定义 MOTD
- 注册命令
- 监听事件

### 哪里找Geyser扩展
在这 [扩展 列表](https://github.com/GeyserMC/GeyserExtensionList)

### 安装扩展
把扩展文件丢到Geyser配置文件下的'extensions'目录

### 新建一个Geyser扩展
可以通过 [Geyser扩展模板](https://github.com/GeyserMC/GeyserExampleExtension/) 进行开发. 有开发基础的人可以自己新建项目.

在 'resources' 目录下 新建 'extension.yml'.

extension.yml:
```yml
id: exampleid
name: ExampleExtension
main: org.geyser.extension.exampleid.ExampleExtension
api: 1.0.0
version: 1.0.0
authors: [ExampleAuthor]
```

这些键的意义如下:
- id:  扩展的id,它应该独一无二,另外还关系到你的命令处理,如 '/exampleid command'.
- name: 扩展的名称
- main: 扩展的主类
- api: api版本
- authors: 作者列表

### 主类

如果有个主类 [implement the 'Extension' interface provided by Geyser](https://github.com/GeyserMC/GeyserExampleExtension/blob/47614575a69bddecb241676215f3c9f9113db304/src/main/java/org/geyser/extension/exampleid/ExampleExtension.java#L10). 
That way, Geyser recognizes the extension, and gives you access to important methods - such as 'logger()', to get your extensions logger. <br>
To see all the methods provided by that interface, see [here](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/extension/Extension.java).

Unlike plugins, extensions do not have a 'onEnable' or 'onDisable' method. Instead, most actions are done in events at different stages during Geyser's lifecycle using events.
Some important ones are:
- `GeyserPreInitializeEvent`: This event is fired when Geyser starts to initialize. If you e.g. need to register extension commands that are configured in your config, 
you would need to load the config here to ensure that your config is ready before the GeyserDefineCommandsEvent is fired. 
- `GeyserPostInitializeEvent`: It is called when Geyser has completed initializing. The bulk of your code should go here, as the GeyserAPI is fully available at this stage.
- `GeyserShutdownEvent`: Called when Geyser is shutting down. You can use this to e.g. save data, or clean up resources.

See below for an example:
```java
@Subscribe
public void onPostInitialize(GeyserPostInitializeEvent event) {
    // example: show that your extension is loading.
    this.logger().info("Loading example extension...");
}
```
If you wish to register custom items, global resource packs (or soon, custom blocks and entities), you will need to subscribe to the event using the @Subscribe annotation,
and register them in the event. You can find an example for custom items [here](/geyser/custom-items/#geyser-extensions). For other events, see [here](/geyser/events) for documentation.

To build your extension, run the Gradle build task, and install the extension.

### 注册命令
To create a command, you would need to use the "Commands" package in the Geyser API. Brief rundown:
- [Command.java](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/command/Command.java)
  This interface represents a command in Geyser - to make one, you can use the CommandBuilder. You can register it with the
  [GeyserDefineCommandsEvent](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/event/lifecycle/GeyserDefineCommandsEvent.java)
- [CommandExecutor.java](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/command/CommandExecutor.java)
  This interface represents a command execute handler in Geyser, and extends the CommandSource interface.
- [CommandSource.java](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/command/CommandSource.java)
  This interface represents a command source in Geyser. It can be used to e.g. send messages to the source, check if the source has permission to execute a command, or get the locale.

```java
Command command = Command.builder(this) // "this" is the extension's main class
        .name("ExampleCommand")
        .bedrockOnly(true)
        .source(CommandSource.class)
        .aliases(List.of("example", "ex"))
        .description("An example command")
        .executableOnConsole(false) 
        .suggestedOpOnly(false)
        .permission("example.command")
        .executor((source, cmd, args) -> {
            // this is the command executor - this is where you would put your code to execute the command.
            // source is the source that executed the command
            // cmd is the command that was executed
            // args are the arguments passed to the command
            source.sendMessage("Hello World");
        })
        .build();
```

To register the command, you would need to subscribe to the GeyserDefineCommandsEvent, and register the command there:
```java
@Subscribe
public void onDefineCommands(GeyserDefineCommandsEvent event) {
    event.register(command);
}
```
If everything went right, you should be able to execute the command in-game by running "/extesionid [command]" - in our case, "/exampleid examplecommand".
Here, it would send "Hello World" to the source that ran the command.
Since we also set aliases, you could also run "/exampleid example" or "/exampleid ex" for the same command.
To provide args, simple run "/exampleid examplecommand [args]" - replacing [args] with the arguments you want to pass to the command.

### Listening to Events
See [here](/geyser/events) for documentation. You do not need to register the event listener, Geyser will do that for you.

---

Facing troubles with extensions?
- Make sure you are using the latest version of Geyser - older versions might not have the latest API changes.
- Add debug prints.
- Ask in the #development channel in the [Geyser Discord server](https://discord.gg/geysermc).