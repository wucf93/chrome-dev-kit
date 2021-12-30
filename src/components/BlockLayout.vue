<script setup lang="ts">
import { NDivider, NInputGroup, NIcon } from 'naive-ui';
import { SwapOutlined } from '@vicons/antd';
import { ref } from 'vue';

type ReverseProps = 'row' | 'row-reverse'

const { title, defaultDirection = 'row' } = defineProps<{ title: string, defaultDirection?: ReverseProps }>();
const emit = defineEmits<{ (e: 'reverse', value: ReverseProps): void }>()

const direction = ref(defaultDirection);

const onReverse = () => {
    direction.value = direction.value === 'row' ? 'row-reverse' : 'row';
    emit('reverse', direction.value);
}

</script>

<template>
    <n-divider title-placement="left">{{ title }}</n-divider>
    <NInputGroup style="display: flex" :style="{ flexDirection: direction }">
        <div class="block-layout_left">
            <slot name="left"></slot>
        </div>
        <div class="block-layout_center">
            <NIcon size="20" @click="onReverse">
                <SwapOutlined></SwapOutlined>
            </NIcon>
        </div>
        <div class="block-layout_right">
            <slot name="right"></slot>
        </div>
    </NInputGroup>
</template>

<style scoped>
.block-layout_left,
.block-layout_right {
    flex: 1 0;
}
.block-layout_center {
    width: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    user-select: none;
}
</style>