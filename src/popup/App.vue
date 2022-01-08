<script setup lang="ts">
import { NTabs, NTabPane } from 'naive-ui';
import Transform from './modules/transform/Index.vue';
import Cookie from './modules/cookie/Index.vue'
</script>

<template>
  <n-tabs modn-value="transform" type="line">
    <n-tab-pane tab="格式转化" name="transform">
      <Transform></Transform>
    </n-tab-pane>
    <n-tab-pane tab="Cookie" name="second">
      <Cookie></Cookie>
    </n-tab-pane>
    <n-tab-pane tab="图床" name="image">图床</n-tab-pane>
  </n-tabs>
</template>
