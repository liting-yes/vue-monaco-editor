# Vue Monaco Editor

monaco-editor with vue3

## Install

```sh
pnpm add @liting-yes/vue-monaco-editor
```

## Usage

### MonacoEditor

```vue
import MonacoEditor from '@liting-yes/vue-monaco-editor'
```

or

```vue
import { MonacoEditor } from '@liting-yes/vue-monaco-editor'
```

#### Props

```ts
interface Props {
  language?: string;
  readOnly?: boolean;
  value?: string;
  options?: monaco.editor.IStandaloneEditorConstructionOptions;
}
```

### MonacoDiffEditor

```vue
import { MonacoDiffEditor } from '@liting-yes/vue-monaco-editor'
```

#### Props

```ts
interface Props {
  language?: string;
  theme?: string;
  values?: string[]; // [original text, modified text]
  readOnly?: boolean;
  options?: monaco.editor.IStandaloneDiffEditorConstructionOptions;
}
```

## LICENSE

[MIT](./LICENSE)
