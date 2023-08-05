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

`connection` can be null if such a player does not exist on Geyser.

`GeyserApi.api()` may be null until after the Geyser plugin enables.

For more information on the Geyser API, see [here](/geyser/api/).

## Using Floodgate
This page has a very simple primer for the Floodgate API. For a full breakdown, see [here](/floodgate/api/).

Add Floodgate's API as a dependency:

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

Get the Floodgate API using:
```java
FloodgateApi api = FloodgateApi.getInstance();
api.isFloodgatePlayer(uuid);
```

For more information on the Floodgate API, see [here](/floodgate/api/).