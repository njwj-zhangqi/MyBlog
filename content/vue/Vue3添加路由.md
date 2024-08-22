---
title: 'Vue3添加路由'
date: 2024-08-22T15:54:13+08:00
draft: true
categories: Vue
slug: 'Vue3添加路由'
---

系列文章：
1. [[vue/Vite搭建Ant Design Vue脚手架|Vite搭建Ant Design Vue脚手架]]

参考链接：[vue3配置router路由并实现页面跳转 - 暴躁老砚 - 博客园 (cnblogs.com)](https://www.cnblogs.com/Yan3399/p/16359021.html)

## 背景
创建好项目之后，想要在左侧加上导航菜单栏，做一个后台管理页面，因此需要用到页面跳转功能，因此需要引入页面路由

## 添加依赖
```bash
pnpm install vue-router@latest --save
```
## 创建路由文件
新建`src/router`文件夹，在里面新建`index.ts`文件
