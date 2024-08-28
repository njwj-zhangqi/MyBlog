在子组件中定义接收的对象类型
```typescript
<script lang="ts">
  import { defineProps } from "vue";
  
  const props = defineProps<{
    article: {
      title: string;
      wordCount: number;
      date: string;
      readingTime: string;
      id: number;
    };
  }>();
// 解析父属性props
const { article } = props;
</script>
```

在子组件的template中使用父组件属性
```typescript
<template>
  <div @click="goToNewBlogPage(article.id)">
    <div>
      <h2>{{ article.title }}</h2>
      <div>
        <span>{{ article.date }}</span>
        <span>{{ article.wordCount }}</span>
        <span>{{ article.readingTime }}</span>
      </div>
    </div>
  </div>
</template>
```


在父组件中传递对象
```typescript
<template>
	<PostTitle v-for="article in articles" :key="article.id" :article="article" />
</template>

<script>
import PostTitle from "../components/PostTitle.vue"
</script>
```