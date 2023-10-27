<template>
  <n-code :code="JSON.stringify(parsed, null, 2)" language="json"></n-code>
</template>

<script setup lang="ts">
import MarkdownIt from "markdown-it";
import { computed } from "vue";
import { NCode } from "naive-ui";

const props = defineProps<{
  md: string;
}>();

const parsed = computed(() => {
  const md = new MarkdownIt();
  return md.parse(props.md, {});
});
</script>
