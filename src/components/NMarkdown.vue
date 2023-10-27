<template>
    {{ parsed }}
</template>

<script setup lang="ts">
import MarkdownIt from 'markdown-it';
import { computed } from 'vue';

const props = defineProps<{
    md: string
}>()

const parsed = computed(() => {
    const md = new MarkdownIt();
    return md.parse(props.md, {});
})
</script>
