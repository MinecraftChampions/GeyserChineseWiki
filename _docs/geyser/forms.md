---
title: Cumulus表单
---

# 什么是 Cumulus?

基岩版的ui叫做`表单`.<br>
Cumulus 是一个 表单 的API库,Geyser以及Floodgate都在使用.<br>
源代码见 [Cumulus](https://github.com/GeyserMC/Cumulus). 你可以通过 [Floodgate API](/floodgate/api/) 或者 [Geyser API](/geyser/api) 使用 Cumulus API.

有三种表单:
* ModalForm
* SimpleForm
* CustomForm

我们将从最简单使用的表单类型讲起,最难使用的表单类型将会放到后面讲解.<br>
我们会讲解如何构造.<br>
最后的最后,我们会讲解如何发送它,以及对响应进行处理.<br>

## ModalForm

这是最简单的一种表单类型,只有固定的几个参数,一般用来入门.<br>
同时也可以用来发送调查问卷,同意或者反对.

<img src="{{ '/img/forms/ModalForm.png' | relative_url }}">

图片中使用的代码如下:

```java
ModalForm.builder()
    .title("Title")//标题
    .content("Content")//内容
    .button1("Button 1")//按钮1
    .button2("Button 2")//按钮2
```

## SimpleForm

它不像ModalForm那么简易,它拥有更多的自定义性.<br>
它依然只有按钮,标题,内容,但是按钮可以带有图像,且没有限制.

<img src="{{ '/img/forms/SimpleForm.png' | relative_url }}">

图片中使用的代码:
```java
SimpleForm.builder()
    .title("Title")//标题
    .content("Content")//内容
    .button("Button without an image")//不带图像的按钮
    .button("Button with URL image", FormImage.Type.URL, "https://github.com/GeyserMC.png?size=200")//带图像,为指定网络路径的按钮
    .button("Button with path image", FormImage.Type.PATH, "textures/i/glyph_world_template.png")//带图像,为资源包路径的按钮
```

## CustomForm

CustomForm就如同它的名字一样,在三个表单类型里自定义性最强.<br>
它有标题,内容,和不同的组件
有关于组件,详见 [组件](https://github.com/GeyserMC/Cumulus/tree/master/src/main/java/org/geysermc/cumulus/component)

<img src="{{ '/img/forms/CustomForm.png' | relative_url }}">

Code used in the image:

```java
CustomForm.builder()
    .title("Title")//标题
    .dropdown("Text", "Option 1", "Option 2")//下滑选项列表,第一个为显示内容
    .input("Input", "placeholder")//输入,文字框外内容和文字框内内容
    .toggle("Toggle")//开关
    .slider("Text", 0, 10, 1, 5)//滑块
```

## 发送表单

当你构建完表单,就需要将表单发送给基岩版玩家了,调用方法如下:
```java
FloodgateApi.getInstance().sendForm(uuid, form); // 或者 #sendForm(uuid, formBuilder)
```
你也可以通过`FloodgatePlayer`实例进行操作
```java
FloodgatePlayer player = FloodgateApi.getInstance().getPlayer(uuid);
player.sendForm(form); // or #sendForm(formBuilder)
```
```java
FloodgatePlayer player = FloodgateApi.getInstance().getPlayer(uuid);
...
player.sendForm(
    CustomForm.builder()
        .title("My cool title")
        .label("10/10 content")
);
```

## 接受响应并处理

当我们发送完表单时,我们就需要接受客户端的相应并作出相应的处理.<br>
要想处理,我们可以使用: `validResultHandler(BiConsumer<Form, ValidFormResponseResult> | Consumer<ValidFormResponseResult>)`, `invalidResultHandler`, `closedResultHandler` 和 `closedOrInvalidResultHandler`.<br>
示例:
```java
SimpleForm.builder()
        .title("标题")
        .content("文字")
        .button("某个按钮")
        .button("第二个按钮")
        //关闭操作
        .closedResultHandler(form -> {
            String content = form.content();
            String title = form.title();
            List<ButtonComponent> buttonList = form.buttons();
            buttonList.forEach(button -> {
                button.image();
                button.text();
            });
        })
        //无效操作处理
        .invalidResultHandler(result -> {
            int index = result.componentIndex();
            ResultType t = result.responseType();
            String errorMessage = result.errorMessage();
            result.isClosed();
            result.isInvalid();
            result.isValid();
        })
        //关闭或无效操作处理
        .closedOrInvalidResultHandler(result -> {})
        //有效操作处理
        .validResultHandler(result -> {
        ButtonComponent button = result.clickedButton();
        });
```

## 表单的i18n

表单上同样可以为不同的区域设置不同的语言<br>
要想添加翻译,可以使用 `translator(BiFunction<String, String, String>)` 或者 `translator(BiFunction<String, String, String>, String)` 例如:
```java
ModalForm form = ModalForm.builder()
    .translator(this::translate, userLanguage)
    .title("Title")
    .content("Content")
    .button1("translate.button1")
    .button2("translate.button2")
    .build();

public String translate(String key, String locale) {
    // 处理
    // 这里的key有4个,就是刚刚定义的Tilte,Content,translate.button1,translate.button2
}
```
也可以直接使用lambada表达式
```java
ModalForm form = ModalForm.builder()
    .translator((key, unused) -> {
        // 处理
        // 这里的key有4个,就是刚刚定义的Tilte,Content,translate.button1,translate.button2
    })
    .title("Title")
    .content("Content")
    .button1("translate.button1")
    .button2("translate.button2")
    .build();
```
