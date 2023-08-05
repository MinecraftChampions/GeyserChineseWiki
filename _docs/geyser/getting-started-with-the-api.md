---
title: 开始
---

首先你需要添加指定仓库到你的项目

**Maven**
```xml
<repository>
    <id>opencollab-snapshot</id>
    <url>https://repo.opencollab.dev/main/</url>
</repository>
```

**Gradle**
```groovy
repositories {
    maven {
        url = uri("https://repo.opencollab.dev/main/")
    }
}
```

## 使用 Geyser

添加Geyser依赖

**Maven**
```xml
<dependency>
    <groupId>org.geysermc.geyser</groupId>
    <artifactId>api</artifactId>
    <version>2.1.2-SNAPSHOT</version>
    <scope>provided</scope>
</dependency>
```

**Gradle**
```groovy
dependencies {
    compileOnly('org.geysermc.geyser:api:2.1.2-SNAPSHOT')
}
```

要想获取基岩版玩家连接的实例，可以使用:

```java
GeyserConnection connection = GeyserApi.api().connectionByUuid(uuid);
```

`connection` 当没有这个玩家时为null

`GeyserApi.api()` 当Geyser没有加载时为null

更多信息详见 [GeyserApi](/geyser/api/).

## 使用 Floodgate
一些内容包含了Floodgate入门, 详见 [FloodgateApi](/floodgate/api/).

首先添加依赖:

**Maven**
```xml
<dependency>
    <groupId>org.geysermc.floodgate</groupId>
    <artifactId>api</artifactId>
    <version>2.2.2-SNAPSHOT</version>
    <scope>provided</scope>
</dependency>
```

**Gradle**
```groovy
dependencies {
    compileOnly('org.geysermc.floodgate:api:2.2.2-SNAPSHOT')
}
```

获取FloodgateApi实例
```java
FloodgateApi api = FloodgateApi.getInstance();
api.isFloodgatePlayer(uuid);
```

详见 [FloodgateApi](/floodgate/api/).