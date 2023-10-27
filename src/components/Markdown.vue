<template>
  <div v-html="html"></div>
</template>

<script setup lang="ts">
import { marked } from "marked";
import { computed } from "vue";

const props = defineProps<{
  md: string;
}>();

const html = computed(() => {
  const html = marked.parse(props.md);
  return html;
});
</script>
