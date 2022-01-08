<script setup lang="ts">
import { NInput, } from 'naive-ui';
import dayjs from 'dayjs';
import { ref, watch } from 'vue';
import BlockLayout from '../../components/BlockLayout.vue'

const isReverse = ref<boolean>(false);
const leftValue = ref<string>();
const rightValue = ref<string>();

watch([leftValue, rightValue, isReverse], () => {
   if (isReverse.value) {
      leftValue.value = !!rightValue.value ? dayjs(rightValue.value).valueOf().toString() : ''
   } else {
      rightValue.value = !!leftValue.value ? dayjs(leftValue.value).format('YYYY-MM-DD HH:mm:ss') : ''
   }
}, { immediate: true })
</script>

<template>
   <BlockLayout title="时间戳转换" @reverse="(value) => isReverse = value === 'row-reverse'">
      <template v-slot:left>
         <NInput
            v-model:value.trim="leftValue"
            :placeholder="isReverse ? '请在左侧输入' : '请输入时间戳'"
            :disabled="isReverse"
         ></NInput>
      </template>
      <template v-slot:right>
         <NInput
            v-model:value="rightValue"
            :placeholder="isReverse ? '请输入需要格式化的日期' : '请在左侧输入'"
            :disabled="!isReverse"
         ></NInput>
      </template>
   </BlockLayout>
</template>
