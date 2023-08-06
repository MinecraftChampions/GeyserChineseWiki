---
title: Geyser 事件列表
---

# Geyser 事件列表
Geyser拥有一个强大的事件系统

详见 [此页面](https://github.com/GeyserMC/Geyser/tree/master/api/src/main/java/org/geysermc/geyser/api/event).

## 事件 类型
要想监听事件就必须把事件监听器注册进Geyser的EventBus.如果你使用的是Geyser扩展编写,可以不用注册进EventBus,仅仅添加`@Subscribe`注解
事件分为以下几种类型:
- [Bedrock](https://github.com/GeyserMC/Geyser/tree/master/api/src/main/java/org/geysermc/geyser/api/event/bedrock): Events that are sent for each connecting Bedrock client,
  基岩版玩家发送的事件,例如`SessionLoginEvent`(基岩版登录到Java服务器事件).
- [Java](https://github.com/GeyserMC/Geyser/tree/master/api/src/main/java/org/geysermc/geyser/api/event/java): 
  Java服务器发送的事件,例如`ServerDefineCommandEvent`(Java服务器发送命令到基岩版客户端).
- [Connection](https://github.com/GeyserMC/Geyser/tree/master/api/src/main/java/org/geysermc/geyser/api/event/connection): 
  与连接会话相关的事件,例如基岩版ping服务器时触发
- [Lifecycle](https://github.com/GeyserMC/Geyser/tree/master/api/src/main/java/org/geysermc/geyser/api/event/lifecycle):
  Geyser运行的事件,例如`GeyserDefineCustomItemsEvent`(发送自定义物品事件)

## 用法:

想要监听事件在监听方法上加上`@Subscribe`注解,例如
```java
@Subscribe
public void onGeyserLoadResourcePacksEvent(GeyserLoadResourcePacksEvent event) {
    logger().info("Loading: " + event.resourcePacks().size() + " resource packs.");
    //event.resourcePacks().add(path-to-pack)
}
```
如果你使用使用非Geyser扩展进行开发,那么监听事件的类必须实现 `EventRegistrar` 接口,并在启动时将事件监听器注册到EventBus
Geyser扩展不需要这样做,只需要在监听的方法加上 `@Subscribe` 注解

**Fabric示例:**
```java
public class ExampleMod implements ModInitializer, EventRegistrar {
    public static final Logger LOGGER = LoggerFactory.getLogger("modid");
    
    @Override 
    public void onInitialize() {
        // 注册Fabric的事件监听器(服务器启动)
        ServerLifecycleEvents.SERVER_STARTING.register((server) -> {
            GeyserApi.api().eventBus().register(this, ExampleMod.class); // 注册监听器
        });
        
        LOGGER.info("Geyser is cool!");
    }
    
    // 添加 @Subscribe 注解
    @Subscribe 
    public void onGeyserPostInitializeEvent(GeyserPostInitializeEvent eventad {
        LOGGER.info("Geyser started!");
    }
}
```
<div class="alert alert-info" role="alert">
    请注意: 不能在`onInitialize`方法里直接加载,因为此时Geyser还没加载
</div>

**Paper/Spigot 插件 示例:**

1. 在 `plugin.yml`, 添加下面这一行:
```yaml
  depend: ["Geyser-Spigot"]
```
这能确保你的插件在Geyser后加载

2. 在你的主类中, 实现 `EventRegistrar` 接口, 并注册事件监听器到Geyser的EventBus
```java
public class ExamplePlugin extends JavaPlugin implements EventRegistrar {
    
    @Override
    public void onEnable(){
        getLogger().info("Registering Geyser event bus!");
        GeyserApi.api().eventBus().register(this, this); // 注册事件监听器
    }

    // 添加 @Subscribe 注解
    @Subscribe
    public void onGeyserPostInitializeEvent(GeyserPostInitializeEvent event) {
        getLogger().info("Geyser started!");
    }
}
```
3. 其实, 也可以这样写,从而做到不添加注解的写法
```java
// 替换 GeyserEvent.class 为你想监听的事件的类
GeyserApi.api().eventBus().subscribe(this, GeyserEvent.class, this::yourMethod);
```

## 事件优先级
这个在属性`Subscribe`注解里(为`postOrder`字段,为`PostOrder`类型(枚举)),如果不进行设置的话默认值将为 `NORMAL`.
实例:
```java
    @Subscribe(postOrder = PostOrder.EARLY)
    public void onEvent(GeyserEvent event) {
        // 做些什么
    }
```
关于优先级列表,详见
[此页面](https://github.com/GeyserMC/Events/blob/master/src/main/java/org/geysermc/event/PostOrder.java).