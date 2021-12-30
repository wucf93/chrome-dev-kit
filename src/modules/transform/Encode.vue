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
        leftValue.value = !!rightValue.value ? decodeURIComponent(rightValue.value) : '';
    } else {
        rightValue.value = !!leftValue.value ? encodeURIComponent(leftValue.value) : '';
    }
}, { immediate: true })
</script>

<template>
    <BlockLayout title="encode/decode" @reverse="(value) => isReverse = value === 'row-reverse'">
        <template v-slot:left>
            <NInput
                v-model:value.trim="leftValue"
                :placeholder="isReverse ? '请在左侧输入' : '请输入需要编码的字符'"
                :disabled="isReverse"
                type="textarea"
                :rows="5"
            ></NInput>
        </template>
        <template v-slot:right>
            <NInput
                v-model:value="rightValue"
                :placeholder="isReverse ? '请输入需要解码的字符' : '请在左侧输入'"
                :disabled="!isReverse"
                type="textarea"
                :rows="5"
            ></NInput>
        </template>
    </BlockLayout>
</template>
