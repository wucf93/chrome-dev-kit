<script setup lang="ts">
import { NInput, NButton, NSpace, NInputGroup, NInputGroupLabel, NDataTable } from 'naive-ui';
import BlockLayout from '../../components/BlockLayout.vue'
import { ref, reactive, } from 'vue';

const cookieValue = ref<string>(document.cookie);
const domain = ref<string>(location.hostname);
const cookieList = ref<chrome.cookies.Cookie[]>([]);

// 复制到剪贴板里
const copy = () => navigator.clipboard.writeText(cookieValue.value);

// con
const columns = [
    { title: 'Key', key: 'name' },
    { title: 'Value', key: 'value' },
    { title: 'Expires', key: 'expires' },
]

chrome.cookies.getAll({}, (cookies) => cookieList.value = cookies)

</script>

<template>
    <BlockLayout title="COOkIE查询与种植">
        <template v-slot:left>
            <NSpace vertical>
                <NSpace>
                    <NInputGroup>
                        <NInputGroupLabel style="width: 75px;">domain</NInputGroupLabel>
                        <NInput placeholder="请输入" v-model.value="domain" style="width: 300px;" />
                        <NButton>确定</NButton>
                    </NInputGroup>
                </NSpace>
                <NDataTable :columns="columns" :data="cookieList"></NDataTable>
                <NSpace justify="end">
                    <NButton @click="copy">复制</NButton>
                </NSpace>
            </NSpace>
        </template>
    </BlockLayout>
</template>