<script setup lang="ts">
import { computed, onMounted, ref } from 'vue'
import * as monaco from 'monaco-editor'
import { isNil } from 'lodash-es'

export interface Props {
  language?: string
  readOnly?: boolean
  value?: string
  options?: monaco.editor.IStandaloneEditorConstructionOptions
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
    emptySelectionClipboard: false,
    find: {
      addExtraSpaceOnTop: true,
    },
    foldingImportsByDefault: false,
    matchOnWordStartOnly: true,
    mouseWheelZoom: true,
    smoothScrolling: true,
    tabSize: 2,
    wrappingIndent: 'indent',
  }),
})

const options = computed(() => {
  const options = props.options ?? {}

  if (!isNil(props.language))
    options.language = props.language
  if (!isNil(props.readOnly))
    options.readOnly = props.readOnly
  if (!isNil(props.value))
    options.value = props.value

  return options
})

const manocaEditorRef = ref()
const editor = ref<monaco.editor.IStandaloneCodeEditor>()
onMounted(() => {
  editor.value = monaco.editor.create(manocaEditorRef.value, options.value)
})

defineExpose({
  monaco,
  editor,
})
</script>

<template>
  <div ref="manocaEditorRef" class="vue-monaco-editor" />
</template>

<style>
.vue-monaco-editor {
  width:100%;
  height:100%;
  border: 1px solid rgba(0, 0, 0, 0.1);
  box-shadow: 0 1px 2px 0 rgb(0 0 0 / 0.05);
}
</style>
