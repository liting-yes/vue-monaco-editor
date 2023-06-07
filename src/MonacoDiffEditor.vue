<script setup lang="ts">
import { computed, onMounted, ref } from 'vue'
import * as monaco from 'monaco-editor'
import { isNil } from 'lodash-es'

export interface Props {
  language?: string
  theme?: string
  values?: string[]
  readOnly?: boolean
  options?: monaco.editor.IStandaloneDiffEditorConstructionOptions
}

const props = withDefaults(defineProps<Props>(), {
  options: () => ({
    automaticLayout: true,
    bracketPairColorization: {
      enabled: true,
      independentColorPoolPerBracketType: true,
    },
    copyWithSyntaxHighlighting: true,
    cursorSmoothCaretAnimation: 'on',
    dimension: {
      width: 600,
      height: 900,
    },
    emptySelectionClipboard: false,
    find: {
      addExtraSpaceOnTop: true,
    },
    foldingImportsByDefault: false,
    matchOnWordStartOnly: true,
    mouseWheelZoom: true,
    smoothScrolling: true,
    tabSize: 2,
  }),
})

const options = computed(() => {
  const options = props.options ?? {}

  if (!isNil(props.theme))
    options.theme = props.theme

  if (!isNil(props.readOnly))
    options.readOnly = props.readOnly

  return options
})

const monacoDiffEditorRef = ref()
const diffEditor = ref<monaco.editor.IStandaloneDiffEditor>()
onMounted(() => {
  const editor = monaco.editor.createDiffEditor(monacoDiffEditorRef.value, options.value)
  if (props.values) {
    editor.setModel({
      original: monaco.editor.createModel(props.values[0] ?? '', props.language),
      modified: monaco.editor.createModel(props.values[1] ?? '', props.language),
    })
  }
  else {
    editor.setModel({
      original: monaco.editor.createModel('console.log("Hello, World !")', props.language),
      modified: monaco.editor.createModel('console.log("Hello, Vuemonaco !")', props.language),
    })
  }
  diffEditor.value = editor
})
defineExpose({
  monaco,
  diffEditor,
})
</script>

<template>
  <div ref="monacoDiffEditorRef" class="vue-monaco-diff-editor" />
</template>

<style>
.vue-monaco-diff-editor {
  width:100%;
  height:100%;
  border: 1px solid rgba(0, 0, 0, 0.1);
  box-shadow: 0 1px 2px 0 rgb(0 0 0 / 0.05);
}
</style>
