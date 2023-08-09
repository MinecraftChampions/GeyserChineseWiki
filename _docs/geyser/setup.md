---
title: 搭建Geyser
page_sidebar: false
---
<div class="row gap-4 mx-0" role="tablist">
  <a class="col btn btn-outline-primary active" href="#" data-bs-toggle="tab" data-bs-target="#host-provider-options" type="button" role="tab" aria-controls="host-provider-options" aria-selected="true">在VPS</a>
  <a class="col btn btn-outline-primary" href="#" data-bs-toggle="tab" data-bs-target="#self-host-options" type="button" role="tab" aria-controls="self-host-options" aria-selected="false">在家用机器</a>
</div>

<div class="tab-content mt-4">
  <div id="host-provider-options" class="tab-pane fade show active" role="tabpanel">
    {% include setup/host-provider.html %}

    {% include setup/instructions/geyser/tabs.html type="provider" %}
  </div>

  <div id="self-host-options" class="tab-pane fade" role="tabpanel">
    {% include setup/instructions/geyser/tabs.html type="selfhost" show_standalone=true %}
  </div>
</div>

<div class="alert alert-warning" role="alert">
  <b>遇到异常?</b> <br>
  请阅读 <a href="/geyser/common-issues/">常见异常</a>.
  如果页面没有记载相关问题,可以加入GeyserMC的 <a href="https://discord.gg/geysermc">Discord</a> 寻求支持.
</div>

<h4 class="mt-4">Further information:</h4>
<ul>
  <li><a href="/geyser/understanding-the-config/">完整的配置文档</a></li>
  <li><a href="/geyser/current-limitations/">目前的一些限制</a></li>
  <li><a href="/geyser/faq/">常见问题</a></li>
</ul>
