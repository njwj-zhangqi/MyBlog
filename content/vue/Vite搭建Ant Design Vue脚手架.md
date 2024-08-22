---
title: 'Vite搭建Ant Design Vue脚手架'
date: 2024-08-22T10:36:45+08:00
draft: true
categories: Vue
slug: Vite搭建Ant Design Vue脚手架
---

参考[Ant Desgin Vue官方链接](https://www.antdv.com/docs/vue/getting-started-cn)
### 使用Vite初始化项目
```bash
pnpm create vite@latest
```

```bash
√ Project name: ... vite-project-test
? Select a framework: » - Use arrow-keys. Return to submit.
    Vanilla
>   Vue
    React
    Preact
    Lit
    Svelte
    Solid
    Qwik
    Others
```
### 安装Ant Design Vue组件
```bash
pnpm i -g ant-design-vue@4.2.3
```
### 引入Ant Design Vue
修改`main.ts`，全局引入
```typescript
import { createApp } from 'vue'
import './style.css'
import App from './App.vue'
import Antd from 'ant-design-vue';
import 'ant-design-vue/dist/reset.css';

const app = createApp(App);

app.use(Antd)
app.mount('#app');
```

### 测试效果
修改`App.vue`，替换`<template>`中的内容
```xml
<template>
  <a-space wrap>
    <a-button type="primary">Primary Button</a-button>
    <a-button>Default Button</a-button>
    <a-button type="dashed">Dashed Button</a-button>
    <a-button type="text">Text Button</a-button>
    <a-button type="link">Link Button</a-button>
  </a-space>
</template>
```