---
title: 'Hugo转换Obsidian链接'
date: 2024-07-05T10:34:07+08:00
draft: true
categories: Hugo
slug: 
---

## 配置Obsidian
将Obsidian的仓库，设置为Hugo的`/content`文件夹

打开 设置 => 文件与链接 => 内部链接类型，选择"基于仓库根目录的绝对路径"

## 添加partials代码片段
在`/layouts/partials`下添加`convert_links.html`文件，内容如下：
```html
<!-- 文件路径：partials/convert_links.html -->

{{- $pattern := `\[\[(.*?)\|(.*?)\]\]` -}}
{{- $linkPattern := `<a href="/$1">$2</a>` -}}
{{- $content := . | replaceRE $pattern $linkPattern | safeHTML -}}
{{- $content -}}
```

## 修改single.html文件
Tips: 如果安装了主题，请不要在主题中修改源文件，在自己的layouts中修改

在本地创建`/layouts/_default/single.html`文件

复制`/themes/PaperMod/layouts/_default/single.html`文件中的内容到文件中

替换代码
```html
  {{- if .Content }}
  <div class="post-content">
    {{- if not (.Param "disableAnchoredHeadings") }}
    {{- partial "anchored_headings.html" .Content -}}
    {{- else }}{{ .Content }}{{ end }}
  </div>
  {{- end }}
```
变成
```html
{{- if .Content }}
<div class="post-content">
  {{- if not (.Param "disableAnchoredHeadings") }}
    {{- partial "anchored_headings.html" -}}
  {{- end }}
  {{- partial "convert_links.html" .Content | safeHTML }}
</div>
{{- end }}
```

## 实现效果
点击跳转到[[hugo/Hugo常用配置|Hugo常用配置]]

## 存在的问题
1. 正则表达式是全局替换，只要在文件中出现了`[[]]`都会被替换。修改成链接中必须带有`|`才会被替换
2. 跳转链接的路径是文件名，因此需要保证每个文件的slug和文件名保持一致，需要修改yaml中的slug，改成`slug: {{  title }}`，slug含义参考[[hugo/Hugo常用配置|Hugo常用配置]]
