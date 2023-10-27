<template>
  <component
    :is="renderFunction(item)"
    v-for="(item, index) in parsed"
    :key="index"
  >
  </component>
</template>

<script setup lang="ts">
import { marked, type Token } from "marked";
import { computed, h, type Component } from "vue";
import {
  NH1,
  NH2,
  NH3,
  NH4,
  NH5,
  NH6,
  NCode,
  NHr,
  NP,
  NText,
  NBlockquote,
  NOl,
  NUl,
  NLi,
  NA,
  NImage,
} from "naive-ui";

const props = defineProps<{
  md: string;
}>();

const parsed = computed(() => {
  const tokens = marked.lexer(props.md, {});
  return tokens;
});

const renderFunction = (token: Token): Component | undefined => {
  if (token.type === "text") {
    return h("span", {}, token.raw);
  }

  if (token.type === "heading") {
    const depthMaps: Record<number, Component> = {
      1: NH1,
      2: NH2,
      3: NH3,
      4: NH4,
      5: NH5,
      6: NH6,
    };
    if (token.tokens && token.tokens.length > 0) {
      return h(depthMaps[token.depth], token.tokens.map(renderFunction));
    } else {
      return h(depthMaps[token.depth], {}, token.text);
    }
  }

  if (token.type === "code") {
    return h(NCode, { code: token.text, language: token.lang });
  }

  if (token.type === "hr") {
    return h(NHr);
  }

  if (token.type === "paragraph") {
    if (token.tokens && token.tokens.length > 0) {
      return h(NP, {}, token.tokens.map(renderFunction));
    } else {
      return h(NP, {}, token.text);
    }
  }

  if (token.type === "strong") {
    if (token.tokens && token.tokens.length > 0) {
      return h(NText, { strong: true }, token.tokens.map(renderFunction));
    } else {
      return h(NText, { strong: true }, token.text);
    }
  }

  if (token.type === "em") {
    if (token.tokens && token.tokens.length > 0) {
      return h(NText, { italic: true }, token.tokens.map(renderFunction));
    } else {
      return h(NText, { italic: true }, token.text);
    }
  }

  if (token.type === "blockquote") {
    if (token.tokens && token.tokens.length > 0) {
      return h(NBlockquote, {}, token.tokens.map(renderFunction));
    } else {
      return h(NBlockquote, {}, token.text);
    }
  }

  if (token.type === "list") {
    if (token.ordered) {
      return h(NOl, {}, token.items.map(renderFunction));
    } else {
      return h(NUl, {}, token.items.map(renderFunction));
    }
  }

  if (token.type === "list_item") {
    if (token.tokens && token.tokens.length > 0) {
      return h(NLi, {}, token.tokens.map(renderFunction));
    } else {
      return h(NLi, {}, token.text);
    }
  }

  if (token.type === "codespan") {
    return h(NText, { code: true }, token.text);
  }

  // FIXME: marked.lexer seems to not support table

  if (token.type === "link") {
    if (token.tokens && token.tokens.length > 0) {
      return h(NA, {href: token.href}, token.tokens.map(renderFunction));
    } else {
      return h(NA, {}, token.text);
    }
  }

  if (token.type === "image") {
    return h(NImage, { src: token.href });
  }


  return undefined;
};
</script>
