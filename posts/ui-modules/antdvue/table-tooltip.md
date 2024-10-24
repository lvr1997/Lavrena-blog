# 在antd-vue的table组件中封装tooltip组件

## 使用场景

> 当表格中某些字段的数据文本过长时

## 具体实现

```vue
<!-- ShowTooltip.vue -->
<template>
    <a-tooltip placement="top" trigger="hover" overlayClassName="table-class" v-model:visible="isShow">
        <template #title>
            <span>{{ content }}</span>
        </template>
        <div class="content" @mouseleave="mouseleave">
            <span ref="contentRef">
                <slot></slot>
            </span>
        </div>
    </a-tooltip>
</template>

<script setup lang="ts">
interface Props {
    content: string
}
  
const props = withDefaults(defineProps<Props>(), {
    content: '',
})

const isShow = ref(false);
const contentRef = ref();
const isShowTooltip = ref(false);
const mouseleave = () => {
    // isShowTooltip.value = false
};

const mouseenter = () => {
    // 关键代码逻辑
    if (contentRef.value.parentNode.offsetWidth > contentRef.value.offsetWidth) {
        isShowTooltip.value = false;
    } else {
        isShowTooltip.value = true;
    }
};
</script>

<style scoped>
.content {
  overflow: hidden;
  white-space: nowrap;
  text-overflow: ellipsis;
}
</style>
```

## 使用

```html
<!-- 如果配置了ellipsis，则自动显示tooltip -->
<ShowTooltip v-if="column.ellipsis" :content="text">{{ text }}</ShowTooltip>
```