<script setup lang="ts">
// src/pages/[...all].vue，被解析为   --> /*  路由，
// 匹配所有未匹配到的路由，省略号后的 all 将为路由名称
const { t } = useI18n()
</script>

<template>
  <div>
    {{ t('not-found') }}
  </div>
</template>

<!-- 以下指定采用的页面布局为 src/layouts/404.vue -->
<route lang="yaml">
meta:
  layout: 404
</route>
