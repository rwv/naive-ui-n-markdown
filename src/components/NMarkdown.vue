<template>
  <div v-for="(item, index) in parsed" :key="index">
    <component :is="renderFunction(item)">
    </component>
  </div>
</template>

<script setup lang="ts">
import MarkdownIt from "markdown-it";
import { computed, h, type Component } from "vue";
import { NH1 } from "naive-ui";

const props = defineProps<{
  md: string;
}>();

const parsed = computed(() => {
  const md = new MarkdownIt();
  return md.parse(props.md, {});
});

const renderFunction = (token: MarkdownIt.Token): Component | undefined => {
  if (token.tag === "h1") {
    return h(NH1, {}, token.content);
  } else {
    return undefined;
  }
};
</script>
