---
title: 从0开始搭建Vue3项目
date: 2024-08-22T16:36:45+08:00
draft: true
categories: Vue
slug: 从0开始搭建Vue3项目
---
## 工具准备
1. 安装Node.js，参考[[vue/前端环境安装#Node JS安装|Node JS安装]]
2. 安装包管理工具，参考[[vue/前端环境安装#pnpm安装|pnpm安装]]

## Vue项目创建
执行命令，由于使用Vue和Typescript，通过--template来指定要使用的模板
```bash
pnpm create vite@latest my-vue3-project -- --template vue-ts
```
按照提示执行：
```bash
cd my-vue3-project
```

```bash
pnpm install
```

```bash
pnpm run dev
```
执行完成，点击[localhost:5173](http://localhost:5173)，访问启动界面，出现Vite + Vue的欢迎界面。

## Vue Router安装
```bash
pnpm install vue-router@4
```
### 新建路由文件
新建路由文件`src/router/index.ts`
```typescript
import { createRouter, createWebHistory, RouteRecordRaw } from 'vue-router';

const routes: Array<RouteRecordRaw> = [
  {
    path: '/',
    name: 'Home',
    component: () => import('../views/Home.vue'), // 确保已经创建了 Home.vue 文件
  },
  {
    path: '/about',
    name: 'About',
    component: () => import('../views/About.vue'), // 确保已经创建了 About.vue 文件
  },
];

const router = createRouter({
  history: createWebHistory(),
  routes,
});

export default router;

```

新建`src/views/Home.vue`
```vue
<template>
    <div>Home</div>
</template>

<script lang='ts' setup name='Home'>
</script>

<style scoped>
</style>
```
新建`src/views/About.vue`
```vue
<template>
    <div>About</div>
</template>

<script lang='ts' setup name='About'>
</script>

<style scoped>
</style>
```
### 配置Vue Router
引入Vue Router组件
```typescript
// src/main.ts
import { createApp } from 'vue';
import App from './App.vue';
import router from './router'; // 引入 router 实例

const app = createApp(App);

app.use(router); // 使用 router

app.mount('#app');
```
## 添加Ant Design Vue组件库
### 安装依赖
```bash
pnpm install ant-design-vue@4
```

```bash
pnpm install @ant-design/icons-vue
```
### 引入组件库
```typescript
// src/main.ts
import { createApp } from 'vue';
import App from './App.vue';
import router from './router';
import Antd from 'ant-design-vue';
import 'ant-design-vue/dist/reset.css'; // 引入 Ant Design Vue 样式

const app = createApp(App);

app.use(router);
app.use(Antd); // 使用 Ant Design Vue

app.mount('#app');
```
### 菜单栏使用
修改`src/App.vue`
```vue
<template>
  <a-layout id="components-layout-demo-side" style="min-height: 100vh">
    <!-- 侧边栏 -->
    <a-layout-sider v-model:collapsed="collapsed" collapsible>
      <div class="logo" />
      <a-menu theme="dark" mode="inline" :default-selected-keys="['1']">
        <a-menu-item key="1">
          <pie-chart-outlined />
          <span>主页</span>
        </a-menu-item>
        <a-menu-item key="2">
          <desktop-outlined />
          <span>关于</span>
        </a-menu-item>
      </a-menu>
    </a-layout-sider>
    <!-- 内容区域 -->
    <a-layout>
      <!-- 头部 -->
      <a-layout-header style="background: #fff; padding: 0" />
      <!-- 页面内容 -->
      <a-layout-content style="margin: 0 16px">
        <div :style="{ padding: '24px', background: '#fff', minHeight: '360px' }">
          <router-view></router-view>
        </div>
      </a-layout-content>
      <!-- 底部 -->
      <a-layout-footer style="text-align: center">
        Ant Design ©2018 Created by Ant UED
      </a-layout-footer>
    </a-layout>
  </a-layout>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import {
  PieChartOutlined,
  DesktopOutlined,
  InboxOutlined,
} from '@ant-design/icons-vue';

export default defineComponent({
  name: 'App',
  components: {
    PieChartOutlined,
    DesktopOutlined,
    InboxOutlined,
  },
  setup() {
    const collapsed = ref<boolean>(false);
    return {
      collapsed,
    };
  },
});
</script>

<style>
#app .logo {
  height: 32px;
  background: rgba(255, 255, 255, 0.2);
  margin: 16px;
}
</style>
```

到这里，页面上已经显示了左侧菜单栏和右侧内容区。
## 菜单跳转
修改`src/App.vue`中的`<a-menu>`标签，使用`<router-link>`关联上路径
```vue
<a-menu theme="dark" mode="inline" :default-selected-keys="['1']">
	<a-menu-item key="1">
	  <router-link to="/">
		<pie-chart-outlined />
		<span>主页</span>
	  </router-link>
	</a-menu-item>
	<a-menu-item key="2">
	  <router-link to="/about">
		<desktop-outlined />
		<span>关于</span>
	  </router-link>
	</a-menu-item>
</a-menu>
```

再次查看页面，点击后，右侧内容区会发生变化。如果发生变化，即表示菜单跳转成功。