<script setup lang="ts">
import { NTabs, NTabPane, NCard } from 'naive-ui';
import Transform from './modules/transform/Index.vue';
</script>

<template>
  <n-tabs modn-value="transform" type="line">
    <n-tab-pane tab="格式转化" name="transform">
      <Transform />
    </n-tab-pane>
    <n-tab-pane tab="Cookie" name="second">Cookie</n-tab-pane>
    <n-tab-pane tab="图床" name="image">图床</n-tab-pane>
  </n-tabs>
</template>

<style>
#app {
  padding: 0 16px;
}
</style>

