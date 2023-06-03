<script setup lang="ts">
import { computed, onMounted, ref } from 'vue'
import * as monaco from 'monaco-editor/esm/vs/editor/editor.api'
import { isNull } from 'lodash-es'

export interface Props {
  value?: string | null
  readOnly?: boolean | null
  options?: monaco.editor.IStandaloneEditorConstructionOptions
}

const props = withDefaults(defineProps<Props>(), {
  value: null,
  readOnly: null,
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
    domReadOnly: true,
    // readOnly: true,
  }),
})

const options = computed(() => {
  const options = props.options ?? {}

  if (!isNull(props.value))
    options.value = props.value
  if (!isNull(props.readOnly))
    options.readOnly = props.readOnly

  return options
})

const manocaEditorRef = ref()
const editor = ref<monaco.editor.IStandaloneCodeEditor>()
onMounted(() => {
  editor.value = monaco.editor.create(manocaEditorRef.value, options.value)
})

defineExpose({
  editor,
})
</script>

<template>
  <div class="vuemonaco">
    <div ref="manocaEditorRef" />
  </div>
</template>

<style scoped></style>
