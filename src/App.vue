<script setup lang="ts">
import { NCode } from "naive-ui";
import NMarkdown from "./components/NMarkdown.vue";
import NMarkdownParsed from "./components/NMarkdownParsed.vue";
import SampleMD from "./sample.md?raw";

const md = SampleMD;
</script>

<template>
  <div style="padding: 5em">
    <header>Naive UI NMarkdown</header>
    <main>
      <n-markdown :md="md" />
      <NMarkdownParsed :md="md" />
    </main>
    <main style="margin-top: 100px">
      <n-code :code="md" />
    </main>
  </div>
</template>
