<script setup lang="ts">
import { NInput } from 'naive-ui';
import { ref, watch } from 'vue';
import BlockLayout from '../../components/BlockLayout.vue'

const isReverse = ref<boolean>(false);
const leftValue = ref<string>();
const rightValue = ref<string>();

watch([leftValue, rightValue, isReverse], () => {
    if (isReverse.value) {
        if (!rightValue.value) return leftValue.value = '';

        try {
            const obj = JSON.parse(rightValue.value.trim());
            leftValue.value = typeof obj === 'object' ? Object.keys(obj).reduce((params, key) => {
                params.append(key, obj[key])
                console.log(323);
                return params
            }, new URLSearchParams()).toString() : '';

        } catch (error) {
            leftValue.value = '';
        }
    } else {
        if (!leftValue.value) return rightValue.value = '';
        let str = '';
        new URLSearchParams(leftValue.value).forEach((key, value) => {
            key && value && (str += `\n  "${key}": "${value}",`);
        })
        rightValue.value = str ? `{${str}\n}` : '';
    }
}, { immediate: true })

</script>

<template>
    <BlockLayout title="查询条件转换" @reverse="(value) => isReverse = value === 'row-reverse'">
        <template v-slot:left>
            <NInput
                :placeholder="isReverse ? '请在左侧输入' : '请输入字符串格式的查询条件，如a=1&b=2&c=3'"
                v-model:value="leftValue"
                type="textarea"
                :rows="5"
                :disabled="isReverse"
            ></NInput>
        </template>
        <template v-slot:right>
            <NInput
                v-model:value="rightValue"
                :disabled="!isReverse"
                type="textarea"
                :rows="5"
                :placeholder="isReverse ? `请输入需要序列化的JSON对象,如：${JSON.stringify({ a: 1, b: 2, c: 3 })}` : '请在左侧输入'"
            ></NInput>
        </template>
    </BlockLayout>
</template>