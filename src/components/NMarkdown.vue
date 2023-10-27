<template>
  <div v-for="(item, index) in parsed" :key="index">
    <component :is="renderFunction(item)">
    </component>
  </div>
</template>

<script setup lang="ts">
import { marked, type Token } from "marked";
import { computed, h, type Component } from "vue";
import { NH1, NH2, NH3, NH4, NH5, NH6 } from "naive-ui";

const props = defineProps<{
  md: string;
}>();

const parsed = computed(() => {
  const tokens = marked.lexer(props.md, {});
  return tokens;
});

const renderFunction = (token: Token): Component | undefined => {
  if (token.type === "heading") {
    const depthMaps: Record<number, Component> = {
        1: NH1,
        2: NH2,
        3: NH3,
        4: NH4,
        5: NH5,
        6: NH6,
    }

    return h(depthMaps[token.depth], {}, token.text);



  } else {
    return undefined;
  }
};
</script>
