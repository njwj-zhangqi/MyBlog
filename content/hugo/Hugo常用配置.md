---
title: 'Hugo常用配置'
date: 2024-06-28T17:23:14+08:00
draft: true
slug: Hugo常用配置
categories: Hugo
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

## 修改右上角的分类和标签
```yaml
menu:
  main:
    - identifier: categories
      name: 分类
      url: /categories/
      weight: 10
    - identifier: tags
      name: 标签
      url: /tags/
      weight: 20
    - identifier: java
      name: Java
      url: /java/
      weight: 30
```
保证identifier唯一，name可以自定义。此时右上角的导航栏变成中文，但是内容页面仍然是英文的Categories

