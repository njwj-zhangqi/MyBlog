---
title: 'Hugo自定义字体'
date: 2024-06-28T16:24:01+08:00
draft: true
slug: hugo-fonts
---

参考链接：[在站点网页中使用霞鹜文楷（LXGW WenKai）](https://hsiaofeng.com/archives/224.html)

## 引入字体样式文件
在`<head>`标签内引入字体CSS。

参考配置Mermaid时引入的JS文件，在`/layouts/partials/extend_head.html`第一行添加内容：
```html
<link rel="stylesheet" href="https://cdn.bootcdn.net/ajax/libs/lxgw-wenkai-webfont/1.6.0/style.min.css" />
<link rel="stylesheet" href="https://cdn.bootcdn.net/ajax/libs/lxgw-wenkai-screen-webfont/1.7.0/style.min.css" />
```

## 引入字体样式
在`/assets/css/extended/custom.css`中添加内容：
```css
body, code {
    /* 原版 */
    font-family: "LXGW WenKai", sans-serif;
    /* 屏幕优化版 */
    font-family: "LXGW WenKai Screen", sans-serif;
}
```

## 修改代码块字体样式
引入字体CSS之后，只能修改正文的字体，代码块的字体没有发生改变。

代码块的class都是以`language-`开头，添加以下内容：
```css
[class^="language-"] {
    /* 原版 */
    font-family: "LXGW WenKai", sans-serif;
    /* 屏幕优化版 */
    font-family: "LXGW WenKai Screen", sans-serif;
}

```

