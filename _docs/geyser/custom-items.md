---
title: 自定义物品
---

# 使用Geyser自定义物品

想要自定义物品(插件端通过`custom_model_data`设置的资源包,一些特定的物品),你必须学会注册它,最简单的方法就是通过[JSON文件映射](#geyser-extensions),或者是使用Java写Geyser的[扩展插件](#geyser-extensions)
需要注意的是:如果你想扩展非原版物品只能使用Geyser扩展

## JSON 映射

1. 首先你应该打开Geyser的配置文件夹,新建 `custom_mappings` 文件夹来存储JSON文件
2. 创建一个后缀名为`.json`的JSON文件,名字无所谓,数量也无所谓,Geyser会自动遍历,它的结构应该如下所示
```json
{
    "format_version": 1,
    "items": {

    }
}
```
3. 要想创建Java物品的扩展,首先你应该在 `items` 项中新建一个键为`minecraft:JAVA_ITEM`的空数组

```json
"minecraft:JAVA_ITEM": [

]
```
4. 这个数组里存储这JSON对象,每个JSON对象代表一个物品的扩展

```json
{
    "name": "my_item"
}
```
5. 这个JSON对象里还可以存储别的属性来匹配(以下属性必须要全部匹配)
    * 自定义模型数据: `custom_model_data` (int)
    * 伤害谓词: `damage_predicate` (int) 这里是物品的伤害
    * 不可破坏: `unbreakable` (boolean)
6. 同时,你这可以添加额外的设置来设置这个物品在基岩版端如何显示. **不是必须**
    * 显示名: `display_name` (string) 默认值: 物品名字
    * 图标: `icon` (string) 默认值: 物品名字
    * 可以在副手: `allow_offhand` (boolean) 默认值: false
    * 图片分辨率: `texture_size` (int) 默认值: 16
    * 渲染偏移: `render_offsets` (object) 配置示例如下(x,y,z必须,其他可选)
    ```json
    "render_offsets": {
        "main_hand": {
            "first_person": {
                "position": {
                    "x": 0,
                    "y": 0,
                    "z": 0
                },
                "rotation": {
                    "x": 0,
                    "y": 0,
                    "z": 0
                },
                "scale": {
                    "x": 0,
                    "y": 0,
                    "z": 0
                }
            },
            "third_person": {

            }
        },
        "off_hand": {

        }
    }
    ```

## Geyser扩展

### 扩展原版物品

1. 首先你需要创建一个`CustomItemOptions`,这里定义了要匹配自定义物品的一些修饰符
```java
CustomItemOptions itemOptions = CustomItemOptions.builder()
        .customModelData(1)
        .damagePredicate(1) //伤害
        .unbreakable(true)
        .build();
```
2. 然后你可以新建一个`CustomItemData`,他定义了这个物品的名字和其他一些修饰符
```java
CustomItemData data = CustomItemData.builder()
        .name("my_item")
        .customItemOptions(itemOptions)
        .build();
```
3. 你可以添加以下这些修饰符
```java
.displayName("displayName"); //默认值: 物品名
.icon("my_icon"); //默认值: 物品名
.allowOffhand(false); //默认值: false
.textureSize(16); //默认值: 16
.renderOffsets(new CustomRenderOffsets(...)); //默认不渲染偏移
```
4. 然后,在Geyser的初始化事件中注册自定义物品
```java
@Subscribe
public void onGeyserPreInitializeEvent(GeyserDefineCustomItemsEvent event) {
    event.registerCustomItem("minecraft:JAVA_ITEM", data);
}
```

### 用GeyserApi定义非原版物品

1. 首先新建一个`NonVanillaCustomItemData`:
```java
NonVanillaCustomItemData data = NonVanillaCustomItemData.builder()
        .name("my_item")
        .identifier("my_mod:my_item")
        .javaId(1)
```
2. `NonVanillaCustomItemData`可以有许多不同的修饰符,详见 [此页面](https://github.com/GeyserMC/Geyser/blob/master/api/src/main/java/org/geysermc/geyser/api/item/custom/NonVanillaCustomItemData.java)
3. 然后,在Geyser的初始化事件中注册自定义物品：
```java
@Subscribe
public void onGeyserDefineCustomItemsEvent(GeyserDefineCustomItemsEvent event) {
    event.register(data);
}
```

## 资源包

1. 新建一个基岩版资源包,教程可以看 [这里](https://wiki.bedrock.dev/guide/project-setup.html#rp-manifest) 或者自行上网搜索.
2. 新建 `textures` 目录.
3. 在 `textures` 文件夹下创建 `item_texture.json` 文件, 里面内容如下:

```json
{
  "resource_pack_name": "MY_PACK_NAME_HERE",
  "texture_name": "atlas.items",
  "texture_data": {
    
  }
}
```
4. 在`texture_data`项填上如下内容,JSON对象的键就是自定义物品的名称

```json
"my_item": {
    "textures": [
        "textures/items/my_item"
    ]
}
```
5. 然后把图片丢到 `textures/items`. 并确保路劲与 `item_texture.json` 设置的一样!
