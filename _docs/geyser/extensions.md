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

在主类中我们应该 [ 实现'Extension'接口](https://github.com/GeyserMC/GeyserExampleExtension/blob/47614575a69bddecb241676215f3c9f9113db304/src/main/java/org/geyser/extension/exampleid/ExampleExtension.java#L10). 
这样,你就能调用一些方法,例如`logger()`<br>
要想知道这个接口中的全部方法,详见 [此页面](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/extension/Extension.java).

不同于插件, Geyser扩展没有 'onEnable' 或者 'onDisable' 方法. 相反, 它类似Forge, 需要监听各种Geyser的生命周期事件.
有这几种事件:
- `GeyserPreInitializeEvent`: 在Geyser准备加载时调用,它是最早触发的一个事件,建议读取配置等操作在这里执行
- `GeyserPostInitializeEvent`: 在Geyser加载完调用,要调用GeyserAPI,请在这里执行
- `GeyserShutdownEvent`: Geyser关闭时调用,建议用来保存数据等.

示例:
```java
@Subscribe
public void (GeyserPostInitializeEvent event) {
    // 输出你个插件这个加载
    this.logger().info("Loading example extension...");
}
```
如果你想要注册自定义资源包和物品,必须添加`@Subscribe`注解,详见 [此页面](/geyser/custom-items/#geyser扩展). 想要知道其它的事件,详见 [此页面](/geyser/events).

### 注册命令
你应该阅读 Geyser API 的 "Commands" 包,与命令有关的类如下:
- [Command.java](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/command/Command.java)
  命令实例
  [GeyserDefineCommandsEvent](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/event/lifecycle/GeyserDefineCommandsEvent.java)
- [CommandExecutor.java](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/command/CommandExecutor.java)
  命令处理程序
- [CommandSource.java](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/command/CommandSource.java)
  命令源,发送者

```java
Command command = Command.builder(this) // 主类
        .name("ExampleCommand")
        .bedrockOnly(true)
        .source(CommandSource.class)
        .aliases(List.of("example", "ex"))
        .description("An example command")
        .executableOnConsole(false) 
        .suggestedOpOnly(false)
        .permission("example.command")
        .executor((source, cmd, args) -> {
            // 操作
            source.sendMessage("Hello World");
        })
        .build();
```

要想注册事件,必须监听`GeyserDefineCommandsEvent`事件
```java
@Subscribe
public void onDefineCommands(GeyserDefineCommandsEvent event) {
    event.register(command);
}
```
注册完之后,可以通过`/扩展id 命令 参数`进行调用

### 监听事件
详见 [事件](/geyser/events)

---

遇到问题?
- 确保使用最新的Geyser.
- 添加日志.
- 在 [Geyser Discord](https://discord.gg/geysermc) 的 #development 频道进行询问.