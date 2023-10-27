<script setup lang="ts">
import { NCode, NGrid, NGi } from "naive-ui";
import NMarkdown from "./components/NMarkdown.vue";
import SampleMD from "./sample.md?raw";
import Markdown from "./components/Markdown.vue";
import hljs from "highlight.js/lib/core";
import javascript from "highlight.js/lib/languages/javascript";
import { NConfigProvider } from "naive-ui";
hljs.registerLanguage("javascript", javascript);

const md = SampleMD;
</script>

<template>
  <div style="padding: 5em">
    <n-config-provider :hljs="hljs">
      <header>Naive UI NMarkdown</header>
      <main>
        <n-grid x-gap="30" :cols="3">
          <n-gi>
            <n-markdown :md="md" />
          </n-gi>
          <n-gi>
            <Markdown :md="md" />
          </n-gi>
          <n-gi>
            <n-code :code="md" />
          </n-gi>
        </n-grid>
      </main>
    </n-config-provider>
  </div>
</template>
