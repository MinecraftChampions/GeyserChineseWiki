---
title: 支持Geyser的 插件/服务商 列表
---

<div class="alert alert-danger" role="alert">
	本列表并不完整,如果想要提交新的 插件/服务商,可以提交一个 <a href="https://github.com/GeyserMC/GeyserWiki/pulls">PR</a> 或者加入GeyserMC的 <a href="https://discord.gg/geysermc">Discord</a>!
</div>

<div class="alert alert-warning" role="alert">
    另外,GeyserMC并不能保证这些 服务商/插件 的安全
</div>

<div class="alert alert-warning" role="alert">
	使用 <i>"免费服务器"</i> 在绝大部分情况下 <i>并不能保证你的使用体验</i>.如果你想要得到更好的体验, 更好控制你的服务器, 学会如何使用配置服务器, 请购买一个VPS.
</div>

<div class="alert alert-info" role="alert">
	除非有说明,否则以下信息皆使用Geyser的最新版本
</div>

## 服务商(提供内置Geyser的服务端)
{% for provider in site.data.providers.built_in %}
* [{{ provider.name}}]({{ provider.url }}){% if provider.description != nil or provider.description_template != nil %} - {{ site.data.providers.description_templates[provider.description_template] }} {{ provider.description }}{% endif %}
{% endfor %}

## 插件(对Geyser进行了适配)
{% for provider in site.data.providers.support %}
* [{{ provider.name}}]({{ provider.url }}){% if provider.description != nil or provider.description_template != nil %} - {{ site.data.providers.description_templates[provider.description_template] }} {{ provider.description }}{% endif %}
{% endfor %}

## 不支持Geyser
{% for provider in site.data.providers.no_support %}
* [{{ provider.name}}]({{ provider.url }}){% if provider.description != nil or provider.description_template != nil %} - {{ site.data.providers.description_templates[provider.description_template] }} {{ provider.description }}{% endif %}
{% endfor %}
