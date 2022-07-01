<script setup lang="ts">
import { ref, onMounted } from "vue"
import { useEditor, EditorContent } from "@tiptap/vue-3"
import StarterKit from "@tiptap/starter-kit"

const editor = useEditor({
  content: "hi there",
  extensions: [StarterKit],
  editorProps: {
    attributes: {
      class: "prose p-4 mx-auto focus:outline-none",
    },
  },
})

const db = ref<IDBDatabase | null>(null)

onMounted(async () => {
  db.value = await getDatabase()
})

async function getDatabase(): Promise<IDBDatabase> {
  return new Promise((resolve, reject) => {
    const open = window.indexedDB.open("zettelkasten")

    open.onerror = (event) => {
      reject("Error opening the database of notes.")
    }

    open.onsuccess = (event: any) => {
      resolve(event.target.result)
    }

    open.onupgradeneeded = (event: any) => {
      event.target.result.createObjectStore("notes")
    }
  })
}
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
