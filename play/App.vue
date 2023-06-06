<script setup lang="ts">
import { MonacoDiffEditor, MonacoEditor } from '../src'
</script>

<template>
  <main>
    <h1>Vue Monaco Editor</h1>
    <h2>ManacoEditor</h2>
    <MonacoEditor value="console.log('Hello, vuemonaco !')" language="javascript" style="height:30vh;" />
    <h2>ManacoDiffEditor</h2>
    <MonacoDiffEditor style="height:30vh;" />
  </main>
</template>

<style scoped>
main {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12px;
  width: 1000px;
  margin: 0 auto;
}

h2 {
  align-self: start;
}
</style>
