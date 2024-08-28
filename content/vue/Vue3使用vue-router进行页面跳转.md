**引入vue-router依赖**
[[vue/Vue3添加vue-router|Vue3添加vue-router]]

参考代码：
```typescript
<script lang="ts" setup>
// 1
import { useRouter } from 'vue-router';

const jumpToNewPage = function (id: number) {
	// 使用路由实例的 push 方法导航到新页面
	router.push("/blog/" + id);
};
</script>
```
