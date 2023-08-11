# GeyserChineseWiki

翻译GeyserMC Wiki

部分翻译借用 SuperiorMC 翻译的[GeyserWiki](https://geyser.superiormc.cn/)

[点击访问](https://geyserwiki.qscraft.top)

本仓库对大部分文本内容进行汉化,同时下载了一些图片存储在此.

另外,本项目与GeyserMC没有任何关系

## Contributing

If you would like to contribute to the wiki, please [open a pull request](https://github.com/GeyserMC/GeyserWiki/pulls).

### Creating a new page

Most documentation is in the docs folder where you can add new page's or edit the current ones.
If a new page is being added make sure you add its page properties at the beginning of the file.
Make sure that the file extension is .md in this case pagetitle.md

### Example page layout

```md
---
layout: page
title: Page title
permalink: /page/pagetitle/
---

# Page title
This is an example page
```

### Adding page to sidebar 

Once you have added the file you can add an sidebar link, All sidebar links + sub links are in the _data/toc.yml file

### Example sidebar structure 

```
- title: Page Title Documentation
  url: "page/"
  links:
    - title: "Pagetitle sub link"
      url: "page/pagetitle/"
      children:
        - title: PageChild sub link
          url: "page/pagetitle/#headerLink"
```
