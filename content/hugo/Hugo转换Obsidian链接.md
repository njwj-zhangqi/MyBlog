---
title: Hugo转换Obsidian链接
date: 2024-06-28T16:16:40+08:00
draft: true
categories: Hugo
slug: Hugo转换Obsidian链接
---

注意：由于编译问题，代码中的`Content`请使用`.Content`替换

## 配置 Obsidian

将 Obsidian 的仓库，设置为 Hugo 的`/content`文件夹

打开 设置 => 文件与链接 => 内部链接类型，选择"基于仓库根目录的绝对路径"

## 添加 partials 代码片段

在`/layouts/partials`下添加`convert_links.html`文件，内容如下：

```go
<!-- 文件路径：partials/convert_links.html -->

{{- $pattern := `\[\[(.*?)\|(.*?)\]\]` -}} {{- $linkPattern := `<a href="/$1">$2</a>` -}} 
{{- $content := . | replaceRE $pattern $linkPattern | safeHTML -}}
 {{-$content -}}
```

## 修改 single.html 文件

Tips: 如果安装了主题，请不要在主题中修改源文件，在自己的 layouts 中修改

在本地创建`/layouts/_default/single.html`文件

复制`/themes/PaperMod/layouts/_default/single.html`文件中的内容到文件中

替换代码

```go
{{- if .Content }}
<div class="post-content">
  {{- if not (.Param "disableAnchoredHeadings") }}
  {{- partial "anchored_headings.html" .Content -}}
  {{- else }}{{ .Content }}{{ end }}
</div>
{{- end }}
```

变成

```go
{{- if .Content }}
<div class="post-content">
  {{- if not (.Param "disableAnchoredHeadings") }}
    {{- partial "anchored_headings.html" .Content }}
  {{- end }}
  {{- partial "convert_links.html" .Content | safeHTML }}
</div>
{{- end }}
```

## 实现效果

点击跳转到[[hugo/Hugo常用配置|Hugo常用配置]]

## 存在的问题

1. 正则表达式是全局替换，只要在文件中出现了`[[]]`都会被替换。修改成链接中必须带有`|`才会被替换
2. 跳转链接的路径是文件名，因此需要保证每个文件的 slug 和文件名保持一致，需要修改 yaml 中的 slug，改成`slug: {{  title }}`，slug 含义参考[[hugo/Hugo常用配置|Hugo常用配置]]
