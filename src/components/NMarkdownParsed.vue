<template>
  <n-code :code="JSON.stringify(parsed, null, 2)" language="json"></n-code>
</template>

<script setup lang="ts">
import { marked } from "marked";
import { computed } from "vue";
import { NCode } from "naive-ui";

const props = defineProps<{
  md: string;
}>();

const parsed = computed(() => {
  const tokens = marked.lexer(props.md, {});
  return tokens;
});
</script>
