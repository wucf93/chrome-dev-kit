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
    <NInputGroup>
        <div :style="{ flexDirection: direction, width: '100%', display: 'flex' }">
            <div class="block-layout_left" v-if="$slots.left" style="flex: 1 0;">
                <slot name="left"></slot>
            </div>
            <div
                class="block-layout_center"
                v-if="$slots.left && $slots.right"
                style="width: 60px;display: flex;align-items: center;justify-content: center;cursor: pointer;user-select: none;"
            >
                <NIcon size="20" @click="onReverse">
                    <SwapOutlined></SwapOutlined>
                </NIcon>
            </div>
            <div class="block-layout_right" v-if="$slots.right" style="flex: 1 0;">
                <slot name="right"></slot>
            </div>
        </div>
        <slot></slot>
    </NInputGroup>
</template>
