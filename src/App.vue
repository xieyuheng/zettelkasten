<script setup lang="ts">
import { useEditor, EditorContent } from "@tiptap/vue-3"
import StarterKit from "@tiptap/starter-kit"

const editor = useEditor({
  content: "hi there",
  extensions: [StarterKit],
  editorProps: {
    attributes: {
      class: "prose m-6 mx-auto focus:outline-none",
    },
  },
})
</script>

<template>
  <div class="flex w-screen h-screen">
    <div
      class="flex flex-col flex-shrink-0 w-64 border-r border-gray-200 bg-gray-100"
    >
      <!-- sidebar -->
    </div>

    <div class="flex flex-col flex-grow">
      <div class="flex flex-col flex-grow overflow-auto">
        <EditorContent :editor="editor" />
      </div>
    </div>
  </div>
</template>
