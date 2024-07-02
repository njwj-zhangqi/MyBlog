---
title: 'Hugo常用配置'
date: 2024-06-28T17:23:14+08:00
draft: true
slug: hugo-used-config
---

## 置顶博客
设置weight属性，默认值为0, 设置成负数即可置顶

## 配置成中文
```yaml
defaultContentLanguage: "zh"
```

## Home页展示所有Section的文章
```yaml
param:
  mainSections: ["java", "posts"]
```