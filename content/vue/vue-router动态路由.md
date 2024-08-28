
定义路由组件，修改`src/router/index.ts`
```typescript

const routes: Array<RouteRecordRaw> = [
  {
	// 动态路由参数 ":id"
    path: '/blog/:id',
    name: 'Blog',
    component: () => import('../views/Blog.vue'), // 确保已经创建了 Home.vue 文件
  }
];
```
路由参数定义的解释
`/blog/:id`：只有一个值，例如`/blog/1`
`/blog/:ids+`：可能含有多个值，例如`/blog/1,2,3`

typescript 强制转换类型：`route.params.id as string`;

获取动态路由值
使用`route.params.id`来获取到动态路由定义时的`/blog/:id`的值，`id`可以任意命名，保持一致即可。


